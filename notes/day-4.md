# Day 4: Installing Applications and Exploring Configuration Files

## Objectives

- **Install a New Application:** Learn how to install applications using online repositories.
- **Explore Standard Directories:** Become familiar with common system directories.
- **Examine Configuration Files:** Review the format and content of key configuration files.


## Basic Commands Practiced

### Package Management

- **`apt search`**  
  Searches for packages based on their description.  
  **Usage Example:**
  ```bash
  apt search <package-name>
  ```

- **`sudo apt install`**  
  Installs a package from the repositories.  
  **Usage Example:**
  ```bash
  sudo apt install <package-name>
  ```

### File Management

- **`mc`**  
  A text-based file manager that simplifies navigating through directories.  
  **Usage Example:**
  ```bash
  mc
  ```

![mc Command demo](/screenshots/day-4/mc-command-demo.PNG)

## Lessons and Notes

- **Configuration Files and Directories:**
  - **`/etc/passwd`:**  
    Contains user account information including the username, user ID, and home directory.
  - **`/etc/ssh/sshd_config`:**  
    The configuration file for the SSH server. It defines settings such as the port number and authentication methods.
  - **`/var/log/auth.log`:**  
    Records authentication events, including both successful and failed login attempts. This log is useful for monitoring system security.


## References
- [Apt vs Apt-Get Difference](https://itsfoss.com/apt-vs-apt-get-difference/)

