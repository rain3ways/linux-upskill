
# Day 3 - Basic Administrative Tasks & User Management

## Objectives
- Change the password of your sudo user.
- Change the hostname.
- Change the timezone.
- Perform basic administrative tasks.
- Manage user accounts.

## User Management Commands

| Command                          | Description                              | Usage Example            |
|----------------------------------|------------------------------------------|--------------------------|
| `adduser <username>`             | Create a new user                        | `adduser rain`           |
| `usermod -aG <group> <username>`  | Add a user to a group                    | `usermod -aG sudo rain`  |
| `passwd <user>`                  | Change the password for a user           | `passwd rain`            |

![Demo User Command](/screenshots/day-3/user-command-pratical.png)

## Using sudo

| Command                  | Description                                                    | Usage Example              |
|--------------------------|----------------------------------------------------------------|----------------------------|
| `sudo cat /etc/shadow`   | Display the file that stores hashed passwords                  | `sudo cat /etc/shadow`     |
| `sudo lastb`             | Show a list of failed login attempts on the system             | `sudo lastb`               |
| `sudo -i` or `sudo -s`    | Start a root shell (with full or limited environment, respectively) | `sudo -i` or `sudo -s`      |

![Sudo -i vs sudo -s](/screenshots/day-3/sudo-i-and-sudo-s.png)

## Administrative Tasks

### Rename Server

Traditionally, you would rename a server by editing two files (`/etc/hostname` and `/etc/hosts`) and then rebooting. However, the modern and recommended way is to use the `hostnamectl` command:

```bash
sudo hostnamectl set-hostname <new-hostname>
````

For cloud servers, the hostname might change after a reboot. To prevent this, edit `/etc/cloud/cloud.cfg` and set:

```
preserve_hostname: true
```

Changing the `preserve_hostname` setting determines whether the system’s hostname remains as configured or is overridden by cloud provider information during a reboot.


### Set Time Zone

- **Check current setting:**
    
    ```bash
    timedatectl
    ```
    
- **List available time zones:**
    
    ```bash
    timedatectl list-timezones
    ```
    
- **Set new time zone (e.g., Asia/Ho_Chi_Minh):**
    
    ```bash
    sudo timedatectl set-timezone Asia/Ho_Chi_Minh
    ```
    
- **Confirm the change:**
    
    ```bash
    timedatectl
    ```
    
![Set server time zone](/screenshots/day-3/set-time-zone.png)

**Warning:** Changing the time zone affects the scheduling of tasks and the timestamping of log files in `/var/log`. A change will result in a noticeable jump in the recorded dates and times.


## Lessons and Notes

- **Global vs. Local Changes:**  
    A global change affects all users, whereas a local change affects only one user.
    
- **User Types:**
    
    - **Root:** A powerful superuser who can execute any command at any level, making global and local changes.
    - **Sudoer:** A regular user permitted to use `sudo`, often with privileges close to root.
    - **Regular User:** A standard user with limited privileges.
- **Password Input:**  
    When running `passwd`, note that no characters will be displayed as you type the password. Always create a strong password and make this a habit as part of your system hardening practices.
    
- **User Groups:**  
    The **wheel** group serves a similar function as the **sudo** group but is typically used in CentOS, Fedora, RHEL, and BSD systems, while the **sudo** group is used in Ubuntu and Debian-based distributions.
    
- **Shell Access with sudo:**
    
    - `sudo -i` creates a new shell with the full environment of the root user.
    - `sudo -s` launches a new shell with root privileges but retains the current user's environment.


## References

- [How To Edit the Sudoers File](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file)
- [Sudo in Ubuntu](https://help.ubuntu.com/community/RootSudo)

