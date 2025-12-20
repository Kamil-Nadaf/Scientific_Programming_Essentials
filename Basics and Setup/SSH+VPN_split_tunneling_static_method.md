# SSH + VPN Split Tunneling Fix (macOS) manual way  
This guide resolves the networking conflict where a VPN intercepting traffic meant for a local or academic Lab Server, causing SSH connections to timeout. It uses a **Static Route** to force traffic for a specific destination IP to bypass the VPN tunnel.

In the following example, I am adding local IP adress of DGS Spark, you can use any other local IP like Datalore or printer etc.

## <span style="color:darkorange;">Configuration Details</span>

* **DGS Spark/Lab Server IP (Target):** `114.212.163.217`
* **Local Gateway IP (Router):** *(You must find this in Step 0)*

## <span style="color:darkorange;">Step 0: Find Your Gateway IP</span>

*Prerequisite: You need to know your physical router's IP address to tell macOS where to send the traffic.*

### Method A: The Command Line Approach

Run this command in Terminal. It is specifically designed to avoid the "bogon" or empty name issue by forcing numeric output (`-n`).

```
route -n get default | grep gateway
```

* **Correct Output:** `gateway: 192.168.1.2` (or similar numbers). <span style="color:dodgerblue;"></span><span style="color:dodgerblue;">*This is my gateaway IP, for you it will be different !*</span>
* **If it says `gateway: bogon`:** You forgot the `-n` flag. Run it again exactly as above.

### Method B: Visual Settings

1. Open **System Settings** (or System Preferences).
2. Click **Wi-Fi** (or Network -\> Ethernet).
3. Click the **"Details..."** button next to your connected network.
4. Look for the field labeled **Router**.
   * *Example:* `192.168.1.1` or `10.0.0.1`.
   * **Write this number down.**

---

## <span style="color:darkgreen;">Type 1: The Manual Alias Method</span>

*Best for: Users who move between locations (home/cafe/lab) or want manual control. You must run this command manually if you disconnect/reconnect the VPN.*

### 1\. Setup (One-time)

Add a permanent alias named <span style="color:red;">vpnspark</span> to your shell configuration.

Replace <span style="color:red;">\<GATEWAY_IP\></span> with the number you found in Step 0 (e.g., 192.168.1.2) and <span style="color:red;">114.212.163.217</span> with the IP adress of the local connection which you want to bypass from VPN.

```
echo "alias vpnspark='sudo route -nv add -host 114.212.163.217 <GATEWAY_IP>'" >> ~/.zshrc
source ~/.zshrc
```

### 2\. Usage

Whenever you restart your computer or toggle your VPN connection, simply open the Terminal and run:

```
vpnspark
```

*(Enter your Mac password when prompted).*

### 3\. Undo / Remove (if you dont want this setting anymore)

To remove the alias:

1. Open your config file: `nano ~/.zshrc`
2. Scroll to the bottom and delete the line starting with `alias vpnspark=...`
3. Press `Ctrl+O` (Enter) to save, and `Ctrl+X` to exit.
4. Reload shell: `source ~/.zshrc`

---

## <span style="color:darkgreen;">Type 2: The Automatic Startup Method</span>

*Best for: Users who work primarily from one location (Home). This runs automatically 60 seconds after boot.*

### 1\. Setup

Copy and paste this **entire block** into your Terminal. It creates a system service (LaunchDaemon) that waits 60 seconds for Wi-Fi/VPN to initialize, then adds the route.

**⚠️ IMPORTANT:** 

* Replace <span style="background-color:gainsboro;"></span><span style="color:red;"></span><span style="color:red;"></span><span style="background-color:gainsboro;">`192.168.2.2`</span><span style="color:red;"></span> in the code below with YOUR specific <span style="color:red;">\<</span><span style="color:red;">Gateway IP\></span> found in Step 0.
* <span style="color:red;">sleep 60 </span>: says that your laptop will initialize bypassing command after 60 seconds when you turn on your laptop and log in so that your vpn gets conected and stabalize the network connection. You can chane the number of seconds to 15 or 120 or anything as you like. 60 seconds is a sweet spot (not too late and not too early)

  

```
# 1. Create the service file with a 60-second delay

sudo tee /Library/LaunchDaemons/com.vpnspark.labroute.plist <<EOF
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "[http://www.apple.com/DTDs/PropertyList-1.0.dtd](http://www.apple.com/DTDs/PropertyList-1.0.dtd)">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.vpnspark.labroute</string>
    <key>ProgramArguments</key>
    <array>
        <string>/bin/sh</string>
        <string>-c</string>
        <string>sleep 60; /sbin/route -n add -host 114.212.163.217 192.168.2.2</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <false/>
</dict>
</plist>
EOF
```



```
# 2. Fix Permissions (Crucial for macOS security)

sudo chown root:wheel /Library/LaunchDaemons/com.vpnspark.labroute.plist
sudo chmod 644 /Library/LaunchDaemons/com.vpnspark.labroute.plist
```



```
# 3. Load the service immediately

sudo launchctl load /Library/LaunchDaemons/com.vpnspark.labroute.plist
```



### 2\. Usage

**Zero touch.** Restart your Mac, log in, and wait **60 seconds**. The connection will be established automatically.

<span style="color:dodgerblue;">*Note: If you manually turn the VPN OFF and ON again, the rule will be wiped. In that case, use the* </span><span style="color:dodgerblue;">***Type 1***</span><span style="color:dodgerblue;"> *alias (*</span><span style="color:dodgerblue;">*`vpnspark`*</span><span style="color:dodgerblue;">*) to restore it without rebooting.*</span>

### 3\. Verification

To check if the rule loaded successfully after a reboot:

```
netstat -nr | grep 114.212.163.217
```

*(If it returns a line of text, the rule is active. If empty, the rule is missing.)*

### 4\. Undo / Remove

To completely disable and delete the automatic script:

```
sudo launchctl unload /Library/LaunchDaemons/com.vpnspark.labroute.plist
sudo rm /Library/LaunchDaemons/com.vpnspark.labroute.plist
```

---

## If you want to add multiple server IPs to bypass the VPN :


### <span style="color:darkorange;">1) Unload the old service</span>

```
sudo launchctl unload /Library/LaunchDaemons/com.vpnspark.labroute.plist 2>/dev/null
sudo rm /Library/LaunchDaemons/com.vpnspark.labroute.plist 2>/dev/null
sudo launchctl unload /Library/LaunchDaemons/com.labserver.route.plist 2>/dev/null
```


### <span style="color:darkorange;">2) Create the New "labserver" Service</span>

Now we create the new file. I have updated the filename to `com.labserver.route.plist` and the internal Label to `com.labserver.route`.

**⚠️ Important:**

* DGS Spark IP : 114.212.163.217
* Datalore IP : 114.212.184.230
* Replace `1.2.3.4` with your 3rd server IP (or remove that line if you don't have one yet).

```
sudo tee /Library/LaunchDaemons/com.labserver.route.plist <<EOF
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "[http://www.apple.com/DTDs/PropertyList-1.0.dtd](http://www.apple.com/DTDs/PropertyList-1.0.dtd)">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.labserver.route</string>
    <key>ProgramArguments</key>
    <array>
        <string>/bin/sh</string>
        <string>-c</string>
        <string>
        sleep 60;
        /sbin/route -n add -host 114.212.163.217 192.168.2.1;
        /sbin/route -n add -host 114.212.184.230 192.168.2.1;
        /sbin/route -n add -host 1.2.3.4 192.168.2.1;
        </string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <false/>
</dict>
</plist>
EOF
```



### <span style="color:darkorange;">3) Set permissions and load</span>

```
sudo chown root:wheel /Library/LaunchDaemons/com.labserver.route.plist
sudo chmod 644 /Library/LaunchDaemons/com.labserver.route.plist
sudo launchctl load /Library/LaunchDaemons/com.labserver.route.plist
```

### <span style="color:darkorange;">4) Verification</span>

After restarting your Mac and waiting 60 seconds:

```
netstat -nr | grep 114.212
```

*(Should show routing entries for your Lab IPs).*

### <span style="color:darkorange;">5) Uninstall</span>

To completely remove the service:

```
sudo launchctl unload /Library/LaunchDaemons/com.labserver.route.plist
sudo rm /Library/LaunchDaemons/com.labserver.route.plist
```