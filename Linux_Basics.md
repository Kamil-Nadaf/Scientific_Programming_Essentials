# Linux Basics Commands

This guide covers essential Linux commands for navigating directories, managing files, and monitoring processes. Each command is explained with practical examples to help you apply them effectively.

## Directory Navigation

These commands help you move through the Linux file system.

- **Change Directory**  
  Moves into the specified directory.  
  ```bash
  cd directory_name
  ```  
  - Example: `cd documents` navigates to the "documents" directory.

- **Go to Parent Directory**  
  Moves up one level to the parent directory.  
  ```bash
  cd ..
  ```  
  - Example: If you're in `/home/user/docs`, `cd ..` takes you to `/home/user`.

- **Go to Home Directory**  
  Returns to your home directory.  
  ```bash
  cd
  ```  
  - Example: `cd` takes you to `/home/user`.

- **Print Working Directory**  
  Displays the full path of your current directory.  
  ```bash
  pwd
  ```  
  - Example: `pwd` might output `/home/user/docs`.

## File Management

These commands allow you to list and manage files and directories.

### Listing Files and Directories
- **List Directory Contents**  
  Shows files and directories in the current directory.  
  ```bash
  ls
  ```  
  - Example: `ls` might display `file1.txt  dir2  script.sh`.

- **Detailed Listing with Sorting**  
  Lists files in long format, sorted by modification time (newest first).  
  ```bash
  ls -lt
  ```  
  - Example: `ls -lt` shows recently modified files at the top.

### File Operations
- **Copy File**  
  Copies a file to a new location.  
  ```bash
  cp source_file destination
  ```  
  - Example: `cp report.txt /backup` copies "report.txt" to "/backup".

- **Move File**  
  Moves a file to a new location.  
  ```bash
  mv source_file destination
  ```  
  - Example: `mv draft.txt /docs` moves "draft.txt" to "/docs".

## Process Monitoring

These commands help you monitor system processes.

- **Monitor System Processes**  
  Provides a real-time view of system resource usage and running processes.  
  ```bash
  top
  ```  
  - Example: `top` displays CPU, memory usage, and active processes dynamically.

## Additional Commands for Coding Efficiency

These extra commands can streamline your coding workflow and improve productivity in Linux.

### File Searching
- **Find Files by Name**  
  Searches for files by name within a directory and its subdirectories.  
  ```bash
  find /path/to/search -name "filename"
  ```  
  - Example: `find /home/user -name "*.py"` locates all Python files.

- **Locate Files Quickly**  
  Finds files using a prebuilt database (update it with `sudo updatedb`).  
  ```bash
  locate filename
  ```  
  - Example: `locate main.py` finds all files named "main.py".

### Text Manipulation
- **View File Contents**  
  Displays the entire contents of a file.  
  ```bash
  cat file_name
  ```  
  - Example: `cat script.sh` shows the contents of "script.sh".

- **Search Text in Files**  
  Recursively searches for a string in files within the current directory.  
  ```bash
  grep -r "search_string" .
  ```  
  - Example: `grep -r "error" .` finds all occurrences of "error".

### Process Management
- **List Running Processes**  
  Displays all currently running processes.  
  ```bash
  ps aux
  ```  
  - Example: `ps aux | grep python` lists Python-related processes.

- **Kill a Process**  
  Terminates a process using its process ID (PID).  
  ```bash
  kill process_id
  ```  
  - Example: `kill 5678` stops the process with PID 5678.

### File Permissions
- **Change Permissions**  
  Modifies file permissions (e.g., read, write, execute).  
  ```bash
  chmod permissions file_name
  ```  
  - Example: `chmod 755 run.sh` makes "run.sh" executable.

### Disk Usage
- **Check Disk Space**  
  Shows available disk space in a readable format.  
  ```bash
  df -h
  ```  
  - Example: `df -h` displays disk usage stats.

- **Check Directory Size**  
  Calculates the total size of a directory and its contents.  
  ```bash
  du -sh directory_name
  ```  
  - Example: `du -sh /logs` shows the size of "/logs".

## Final Notes
For more details, use the `man` command (e.g., `man ls`) to access full documentation. Practice these commands to build your Linux proficiency!