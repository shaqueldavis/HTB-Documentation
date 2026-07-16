#  Linux Fundamentals

## $\color{blue}{\text{Objective}}$


This module covers the fundamentals required to work comfortably with the Linux operating system and shell.

### Skills Learned

This module covers:

- Linux structure
- Using the shell
- Navigating the Linux operating system
- Working with files and directories
- Linux administration
- Service management
- Permissions management

### Tools Used
 📁 Navigation & File Management
- **cd** – Changes the current working directory. Fundamental for navigating the Linux file system.
- **pwd** – Prints the current working directory. Useful for confirming your location before creating, modifying, or deleting files.
- **ls** – Lists the contents of a directory. One of the most frequently used commands for navigating Linux.
- **ls -la** – Lists all files, including hidden files, with detailed information such as permissions, ownership, and timestamps. Helpful for inspecting directories.
- **ls -i** – Displays the inode number for each file. Useful for understanding how Linux stores files and identifying hard links.
- **find** – Searches for files and directories based on criteria like name, size, type, or permissions. One of Linux's most powerful file management tools.
- **cat** – Displays the contents of files in the terminal. Commonly used to quickly read configuration files or combine multiple files.

🔎 Searching & Text Processing
- **grep** – Searches files and command output for specific text or patterns. Essential for filtering logs, configuration files, and troubleshooting.
- **sed** – A stream editor used to search, replace, and transform text. Powerful for automating edits in files and scripts.
- **sort -u** – Sorts data alphabetically while removing duplicate entries. Useful for organizing output and identifying unique values.
- **wc -l** – Counts the number of lines in a file or command output. Commonly used to measure file size, count log entries, or summarize results.
- **echo** – Prints text or variable values to the terminal. Commonly used for testing, scripting, and creating files.

🖥️ System Information
- **uname** – Displays information about the operating system and kernel. Useful for identifying system architecture and kernel version.
- **env** – Displays environment variables used by the operating system and applications. Helpful for troubleshooting and understanding system configuration.
- **ps aux** – Displays all running processes along with resource usage and ownership information. Essential for monitoring system activity and troubleshooting applications.
- **systemctl** – Controls and manages system services on Linux systems using systemd. Essential for starting, stopping, restarting, and checking service status.
- **lsblk** – Lists block storage devices such as hard drives, SSDs, and USB storage. Useful for identifying disks, partitions, and mounted storage devices.

🌐 Networking
- **ip link** – Displays and manages network interfaces. Commonly used to verify network adapters and troubleshoot connectivity issues.
- **curl** – Transfers data to and from servers using URLs. Frequently used for testing APIs, downloading files, and troubleshooting web services.

📦 Package Management
- **dpkg** – Manages software packages on Debian-based systems such as Ubuntu. Commonly used to install, remove, and verify installed packages.
- **npm** – Node Package Manager used to install and manage JavaScript packages and project dependencies. Important when working with Node.js applications.

🛠️ Utilities
- **which** – Displays the location of an executable command in the system's PATH. Helpful for verifying installed programs and troubleshooting command execution.
- **--help** – Displays built-in documentation for a command, including syntax and available options. One of the fastest ways to learn unfamiliar commands.
- **php -S** – Starts PHP's built-in development web server. Useful for quickly testing PHP applications without configuring a full web server.

## $\color{blue}{\text{Steps}}$

### System Information

$\color{green}{\text{Question:}}$ Find out the machine hardware name and submit it as the answer. <br> 
$\color{green}{\text{Answer:}}$ x86_64 <br> 
$\color{green}{\text{Process:}}$ <br>
- uname --help | grep -i machine <br>
- uname -m

$\color{green}{\text{Question:}}$ What is the path to htb-student's home directory? <br>
$\color{green}{\text{Answer:}}$ /home/htb-student <br>
$\color{green}{\text{Process:}}$ <br>
- cd ~ <br>
- pwd 

$\color{green}{\text{Question:}}$ What is the path to the htb-student's mail? <br>
$\color{green}{\text{Answer:}}$ /var/mail/htb-student <br>
$\color{green}{\text{Process:}}$ <br>
- /var This directory contains variable data files such as log files, email in-boxes, web - - application related files, cron files, and more. <br>
- env | grep mail <br>
- Or… <br>
- find / type -d -name  mail 2>/dev/null | grep var 

$\color{green}{\text{Question:}}$ Which shell is specified for the htb-student user? <br>
$\color{green}{\text{Answer:}}$ /bin/bash <br>
$\color{green}{\text{Process:}}$ <br>
- /bin Contains essential command binaries. <br>
- Echo $SHELL 

$\color{green}{\text{Question:}}$ Which kernel release is installed on the system? <br>
$\color{green}{\text{Answer:}}$ 4.15.0 <br>
$\color{green}{\text{Process:}}$ <br>
- uname --help | grep kernel <br>
- uname -r

$\color{green}{\text{Question:}}$ What is the name of the network interface that MTU is set to 1500? <br>
$\color{green}{\text{Answer:}}$ ens192 <br>
$\color{green}{\text{Process:}}$ <br>
- ip link | grep "mtu\ 1500"



### Navigation

 $\color{green}{\text{Question:}}$ What is the name of the hidden "history" file in the htb-user's home directory? <br>
$\color{green}{\text{Answer:}}$ .bash_history <br>
$\color{green}{\text{Process:}}$ <br>
- ls -la | grep -i history

 $\color{green}{\text{Question:}}$ What is the index number of the "sudoers" file in the "/etc" directory? <br>
$\color{green}{\text{Answer:}}$ 147627 <br>
$\color{green}{\text{Process:}}$ text_here<br>
- ls --help | grep index<br>
- ls -i /etc/sudoers




### Working with Files and Directories

 $\color{green}{\text{Question:}}$ What is the name of the last modified file in the "/var/backups" directory?<br>
$\color{green}{\text{Answer:}}$ apt.extended_states.0<br>
$\color{green}{\text{Process:}}$ <br>
- ls --help | grep time<br>
- ls -lt | head -2

 $\color{green}{\text{Question:}}$  What is the inode number of the "shadow.bak" file in the "/var/backups" directory?<br>
$\color{green}{\text{Answer:}}$ 265293<br>
$\color{green}{\text{Process:}}$ <br>
- ls --help | grep inode<br>
- ls -i /var/backups/shadow.bak




 

### Find Files and Directories

 $\color{green}{\text{Question:}}$  What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?<br>
$\color{green}{\text{Answer:}}$ 00-mesa-defaults.conf<br>
$\color{green}{\text{Process:}}$ <br>
- find / -type f -newermt 2020-03-03 -size +25k -size -28k -name "*.conf" 2>/dev/null<br>

 $\color{green}{\text{Question:}}$ How many files exist on the system that have the ".bak" extension?<br>
$\color{green}{\text{Answer:}}$ 4<br>
$\color{green}{\text{Process:}}$ <br>
- find / -type f -name "*.bak" 2>/dev/null | wc -l

 $\color{green}{\text{Question:}}$ Submit the full path of the "xxd" binary.<br>
$\color{green}{\text{Answer:}}$ /usr/bin/xxd<br>
$\color{green}{\text{Process:}}$ <br>
- find / -type f -name "*xxd*" 2>/dev/null









 

### File Descriptors and Redirections

 $\color{green}{\text{Question:}}$ How many total packages are installed on the target system?<br>
$\color{green}{\text{Answer:}}$ 32<br>
$\color{green}{\text{Process:}}$ <br>
- find / -type f -name "*.log" 2>/dev/null | wc -l<br>



 $\color{green}{\text{Question:}}$ How many files exist on the system that have the ".log" file extension?<br>
$\color{green}{\text{Answer:}}$ 737<br>
$\color{green}{\text{Process:}}$ <br>
- dpkg -l | grep 'ii' | wc -l<br>
- dpkg is the low-level package management tool used by Debian-based Linux systems.<br>
- The first two letters show package status: ii = installed. rc = removed. un = not installed. <br>



### Filter Contents



 $\color{green}{\text{Question:}}$ How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)<br>
$\color{green}{\text{Answer:}}$ 7<br>
$\color{green}{\text{Process:}}$ <br>
- ss -tln | awk '/0.0.0.0/ {print $4}' | grep 0.0.0.0 | wc -l<br>
  - ss stands for Socket Statistics. It shows you: Which network services are running, what ports they’re using, and how they’re communicating.<br>
    - -t → TCP<br>
    - -l → Listening<br>
    - -n → Numeric (no DNS)<br>
  - awk '/0.0.0.0/ {print $4}' = print only lines containing 0.0.0.0 anywhere in the line but only print column 4, the local address:port column.<br>
  - Grep 0.0.0.0 = further filter for only lines with 0.0.0.0 <br>
  - Wc -l = count lines

$\color{green}{\text{Question:}}$ Determine what user the ProFTPd server is running under. Submit the username as the answer.<br>
$\color{green}{\text{Answer:}}$ proftpd<br>
$\color{green}{\text{Process:}}$ <br>
- ps aux | head -1<br>
  - Ps displays running processes<br>
  - ps → displays running processes<br>
  - a → show processes from all users<br>
  - u → show the user column<br>
  - x → include background services (daemons)<br>
  - Head -1 show first column to reveal the user column field<br>
- Ps aux | grep -i proftpd<br>
  - Grep -i proftpd → filter only lines related to ProFTPd, case insensitive

 $\color{green}{\text{Question:}}$  Use cURL from your Pwnbox (not the target machine) to obtain the source code of the "https://www.inlanefreight.com" website and filter all unique paths (https://www.inlanefreight.com/directory" or "/another/directory") of that domain. Submit the number of these paths as the answer.<br>
$\color{green}{\text{Answer:}}$ 34<br>
$\color{green}{\text{Process:}}$ <br>
  - curl -s https://www.inlanefreight.com | \<br>
  - grep -oE 'https://www\.inlanefreight\.com[^"'\'' >]+' | \<br>
  - sed 's|https://www\.inlanefreight\.com||' | \<br>
  - sort -u | \<br>
  - wc -l
- curl -s https://www.inlanefreight.com | grep -oE 'https://www\.inlanefreight\.com[^"'\'' >]+' | sed 's|https://www\.inlanefreight\.com||' | sort -u | wc -l


### User Management


 $\color{green}{\text{Question:}}$ Which option needs to be set to create a home directory for a new user using "useradd" command?<br>
$\color{green}{\text{Answer:}}$ -m<br>
$\color{green}{\text{Process:}}$ <br>
- useradd --help | grep "home"

 $\color{green}{\text{Question:}}$ Which option needs to be set to lock a user account using the "usermod" command? (long version of the option)<br>
$\color{green}{\text{Answer:}}$ --lock<br>
$\color{green}{\text{Process:}}$ <br>
- usermod --help | grep lock<br>

 $\color{green}{\text{Question:}}$ Which option needs to be set to execute a command as a different user using the "su" command? (long version of the option)<br>
$\color{green}{\text{Answer:}}$ --command<br>
$\color{green}{\text{Process:}}$ <br>
- su --help | grep command




 

### Service and Process Management


 $\color{green}{\text{Question:}}$ Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer.<br>
$\color{green}{\text{Answer:}}$ snapd.apparmor.service<br>
$\color{green}{\text{Process:}}$ <br>
- Systemctl<br>
- /AppArmor<br>
- [scroll to the left with the arrow keys]
 

### Task Scheduling


$\color{green}{\text{Question:}}$  What is the Type of the service of the "dconf.service"?<br>
$\color{green}{\text{Answer:}}$ dbus<br>
$\color{green}{\text{Process:}}$ <br>
- systemd has a fixed, standardized directory structure. Service files live in:<br>
  - /usr/lib/systemd/<br>
  - /etc/systemd/<br>
  - /lib/systemd/<br>
    - And within those:<br>
      - system/   → system-wide services  <br>
      - user/     → user-session services<br>
- find /usr/lib/systemd /lib/systemd /etc/systemd -name "*dconf*"<br>
- cat /usr/lib/systemd/user/dconf.service | grep -i type
 

### Working with Web Services


 $\color{green}{\text{Question:}}$ Find a way to start a simple HTTP server inside Pwnbox or your local VM using "npm". Submit the command that starts the web server on port 8080 (use the short argument to specify the port number).<br>
Hint: Npm is a package manager that allows you to download a basic web server package. This package also provides the option to specify the port. No need to install it. How would the command look after installing the corresponding package with a specified listening port?<br>
$\color{green}{\text{Answer:}}$ http-server -p 8080<br>
$\color{green}{\text{Process:}}$ <br>
- npm --help | grep install<br>
- npm install --help | grep global<br>
- sudo npm install -g http-server<br>
  - Use sudo because your installing globally <br>
- Which http-server <br>
  - To make sure http-server is installed<br>
- http-server -p 8080


$\color{green}{\text{Question:}}$  Find a way to start a simple HTTP server inside Pwnbox or your local VM using "php". Submit the command that starts the web server on the localhost (127.0.0.1) on port 8080.<br>
$\color{green}{\text{Answer:}}$ php -S 127.0.0.1:8080<br>
$\color{green}{\text{Process:}}$ <br>
- php --help | grep -ie "-s"<br>
- php -S 127.0.0.1:8080<br>
  - Start a simple web server<br>
  - Listen only on localhost<br>
  - Use port 8080

 
### File System Management


$\color{green}{\text{Question:}}$ How many partitions exist in our Pwnbox? (Format: 0)<br>
$\color{green}{\text{Answer:}}$ 3<br>
$\color{green}{\text{Process:}}$ <br>
- lsblk | grep part | wc -l<br>
  - lsblk = list block devices<br>
    - It shows:<br>
      - Disks (e.g., sda)<br>
      - Partitions (e.g., sda1, sda2)<br>
      - Mount points (e.g., /, /boot)<br>
  - partitions are the lines with: TYPE column = part<br>
    - So grep for part<br>
  - Then count the lines with wc -l<br>
- Option 2:<br>
  - sudo fdisk -l<br>
    - List All Disks & Partitions<br>
    - Every line starting with /dev/ = 1 partition<br>
  - sudo fdisk -l | grep “^/dev/” | wc -l<br>
    - The ^ used in the grep command means match the beginning of the line<br>
    - Wc- l counts the lines

