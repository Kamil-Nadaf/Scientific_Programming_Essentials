# Server or Cluster

This document gives the basic commands for connecting to a remote server or cluster and copying files. Servers and Clusters are usually linux based so our linux commands work here.

Suppose you have an account on the server in the format `name@id`.

## Connecting to the Server

- **SSH with X11 Forwarding**  
  Connects to the server and enables graphical applications.  
  ```bash
  ssh -X -Y name@id
  ```  
  - Example: `ssh -X -Y user@server.example.com`  
  - After running the command, enter your password when prompted.

**Note**: `-X` enables X11 forwarding, and `-Y` allows trusted X11 forwarding for improved performance with graphical applications.

**Now you are successfully connected to the Server/Cluster**

**Note**: Be careful while using servers and clusters specially when you don't have an access to sudo command. One mistake can crash the server so ask for help from supervoiser whenever needed. 

I will quote the message which came when first time I logged in into our servers at Indian Institute of Astrophysics (IIA), 

          "With Great Power Comes Great Responsibilty"

## Copying Files from Server to Local Machine

- **Secure Copy (SCP)**  
  Copies a file from the server to your local machine.  
  ```bash
  scp name@id:path_to_the_file_in_that_server local_path
  ```  
  - Example: `scp user@server.example.com:/path/to/file.txt /local/directory`  
  - This copies "file.txt" from the server to "/local/directory" on your machine.

**Note**: Specify the full path to the file on the server and the destination on your local machine.

## Additional Useful Commands

These commands can improve your efficiency when working with remote servers:

- **Copy Directory from Server**  
  Recursively copies an entire directory from the server to your local machine.  
  ```bash
  scp -r name@id:remote_directory local_path
  ```  
  - Example: `scp -r user@server.example.com:/path/to/dir /local/dir`

- **Upload File to Server**  
  Copies a file from your local machine to the server.  
  ```bash
  scp local_file name@id:remote_path
  ```  
  - Example: `scp /local/file.txt user@server.example.com:/remote/dir`

- **Run Command Remotely**  
  Executes a command on the server without logging in.  
  ```bash
  ssh name@id 'command'
  ```  
  - Example: `ssh user@server.example.com 'ls -l'`

- **Check Disk Usage**  
  Displays disk space usage on the server.  
  ```bash
  df -h
  ```

- **Monitor Processes**  
  Shows real-time system resource usage and processes.  
  ```bash
  top
  ```

## Final Notes
These commands provide a solid starting point for interacting with remote servers. For more information, consult `man ssh` or `man scp` in your terminal. Practice these to optimize your workflow!