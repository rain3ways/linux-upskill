# Day 1: Linux Server Setup & Basic Commands

## Objectives

- **Set Up a Server:** Create a new server (using an EC2 instance on AWS).
- **Connect & Log In:** Use SSH to connect to your server.
- **Perform Basic Checks:** Run common Linux commands to verify your server’s status and gather system information.



## Server Setup and Login

### Creating the Server

- **AWS EC2 Instance:**  
    Launch an EC2 instance on AWS following your preferred configuration.

### Logging in via SSH

- **SSH Command Example:**  
    Replace `<key_pair>`, `<user>`, and `<ip_address>` with your key file, username, and server IP address respectively.
    
    ```bash
    ssh -i <key_pair> <user>@<ip_address>
    ```
    
    _Alternatively, if your key is stored in your default SSH directory:_
    
    ```bash
    ssh -i ~/.ssh/id_rsa <user>@<ip_address>
    ```

![Ssh-to-ubuntu-server](/screenshoots/day-1/ssh-to-ubuntu-server.png)

- **SSH Client Configuration Tip:**  
    You can simplify future logins by configuring the `~/.ssh/config` file (see the "Lessons and Notes" section below).



## Installing Basic Packages

Before running any commands, update your package lists and upgrade installed packages:

```bash
sudo apt update && sudo apt upgrade
```

## Basic Commands Practiced

### A. System Information

|**Command**|**Description**|**Usage Example**|
|---|---|---|
|`lsb_release` (or `cat /etc/os-release`)|Displays the Linux distribution and version information|`lsb_release -a`|
|`uname -a`|Prints detailed system information|`uname -a`|
|`uptime`|Shows how long the system has been running|`uptime -p`|
|`whoami`, `who`, `w`|`whoami` shows your current username; `who` lists logged-in users; `w` provides additional activity details|`whoami`, `who`, `w`|

![General-information-server-command](/screenshoots/day-1/general-information-server.png)

### B. Hardware Information

| **Command** | **Description**                                                 |
| ----------- | --------------------------------------------------------------- |
| `lscpu`     | Displays detailed information about the CPU architecture.       |
| `lsblk`     | Lists block devices such as hard drives or SSDs.                |
| `lspci`     | Lists all PCI devices (e.g., graphics cards, network adapters). |
| `lsusb`     | Lists all connected USB devices.                                |

---

### C. System Measurements

|**Command**|**Description**|**Usage Example**|
|---|---|---|
|`free`|Checks memory usage.|`free -h`|
|`vmstat`|Displays system memory statistics and process information.|`vmstat`|
|`top`|Displays running processes and resource usage (similar to Task Manager).|`top`|
|`htop`|Provides an interactive view of processes (may require installation).|`htop`|
|`df`|Shows disk space usage.|`df -h`|
|`du`|Estimates the size of files and directories.|`du -h`|

![Htop-command-demo](/screenshoots/day-1/htop-command.png)

![Disk-usage](/screenshoots/day-1/disk-usage.png)

### D. Network Usage

|**Command**|**Description**|
|---|---|
|`ifconfig` (or `ip address`)|Lists network interfaces along with their IP addresses. (Note: `ifconfig` is part of the `net-tools` package.)|
|`netstat -i`|Displays a list of network interfaces with basic statistics such as packets sent/received, errors, and dropped packets.|
|`ifstat`|Provides real-time statistics of network traffic (bytes sent/received over a specified period).|
|`sudo iftop -i eth0`|Monitors network traffic in real time, showing active connections and bandwidth usage between IP addresses. Replace `eth0` with your actual interface if needed.|

![Network-usage-command](/screenshoots/day-1/network-measure-iftop.png)

## Lessons and Notes

- **Command Prompt Symbols:**
    
    - `$` indicates a standard (non-root) user prompt.
    - `#` indicates the root user prompt.
- **SSH Configuration:**  
    Simplify your login process by adding an entry to your `~/.ssh/config` file. For example:
    
    ```
    Host rain
        HostName <ip_address>
        User <user>
        IdentityFile ~/.ssh/id_rsa
    ```
    
    This lets you simply connect by typing `ssh rain`.
    
- **Terminology:**
    
    - **Block Devices:** Devices that store data in blocks (e.g., hard drives, SSDs).
    - **PCI Devices:** Hardware components connected via the PCI/PCIe bus (e.g., graphics cards, network cards).

---

## Issues Encountered and Solutions

### Issue 1: Unable to SSH into the AWS Server

- **Potential Causes & Solutions:**
    - **Internet Gateway:**  
        Ensure that an Internet Gateway is attached to your VPC and that your Route Table is configured correctly.
    - **Key-Pair File Location:**  
        Verify that you are in the correct directory containing your key-pair file. Either navigate to that directory or copy the key-pair file to your current working directory before running the SSH command.

### Issue 2: Missing Commands (`ifconfig`, `ifstat`, `iftop`)

- **Solution:**  
    Install the necessary packages using:
    
    ```bash
    sudo apt install net-tools ifstat iftop
    ```
    
    This will provide `ifconfig` (from net-tools) and the other commands.

---

## References

- [**SSH Client Configuration:**](https://linuxize.com/post/using-the-ssh-config-file/) Refer to official SSH documentation or trusted Linux tutorials for further details on setting up and using SSH effectively.
- [**Linux Hardware Information:**](https://opensource.com/article/19/9/linux-commands-hardware-information) Look up additional resources on Linux commands for displaying hardware details if needed.
