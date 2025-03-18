# Day 13 - Setting Up a Help-Desk User with Limited `sudo` Privileges in Linux

## Objectives

- Learn how to create a new user and a new group in Linux.
- Understand how to assign a user to groups for permission management.
- Configure `sudo` privileges to allow a help-desk user to perform specific tasks: checking system status, checking disk space, and rebooting the system.
- Explore the basics of Linux user management and test the setup.

## Basic Commands Practiced



| Command            | Description                                           | Usage Example                                      |
|--------------------|-------------------------------------------------------|----------------------------------------------------|
| `adduser`          | Creates a new user account with a home directory.     | `sudo adduser helen`                               |
| `passwd`           | Sets or changes a user’s password manually.           | `sudo passwd helen`                                |
| `groupadd`         | Creates a new group.                                  | `sudo groupadd helpdesk`                           |
| `usermod -a -G`    | Adds a user to an existing group.                     | `sudo usermod -a -G helpdesk helen`                |
| `groups`           | Shows the groups a user belongs to.                   | `groups helen`                                     |
| `sudo su`          | Switches to another user account for testing.         | `sudo su helen`                                    |
| `visudo`           | Edits the `/etc/sudoers` file safely.                 | `sudo visudo`                                      |
| `df -h`            | Checks disk space in a human-readable format.         | `df -h`                                            |
| `sudo reboot`      | Reboots the system (requires `sudo` privileges).      | `sudo reboot`                                      |
| `exit`             | Exits the current user session.                       | `exit`                                             |

## Lessons and Notes

- **Creating a New User**:
  - I created a user named `rain` with `sudo adduser rain`. This command set up a home directory (`/home/rain`) and added an entry to `/etc/passwd`. If the command didn’t prompt for a password, I used `sudo passwd rain` to set it manually.
  - Linux stores user data in text files: `/etc/passwd` (users), `/etc/group` (groups), and `/etc/shadow` (password hashes). I checked these files with `sudo less` to see how they work.

![Creat user rain](/screenshots/day-13/add-user-rain.png)

- **Creating a New Group**:
  - I made a new group called `devops` using `sudo groupadd devops` to group devops staff together.
  - T created a new user `wind` directly into devops group, with `sudo adduser --ingroup devops wind`. 

![Create devops group and add new user Wind to it](/screenshots/day-13/create-new-group-and-add-user.png)

- **Managing Groups**:
  - I added `rain` to the `devops` group with `sudo usermod -a -G devops rain`. The `-a` flag ensures I append the group without overwriting existing memberships.
  - To verify, I ran `groups rain` and saw his group memberships.

![Add user rain to devops group](/screenshots/day-13/add-second-group-to-user.png)

- **Setting Up `sudo` Privileges**:
  - My goal was to let `rain` check system status (he can already run `df -h` as a regular user) and reboot the system with `sudo reboot`, but not give his full admin powers.
  - I used `sudo visudo` to edit `/etc/sudoers` and added this line:
    ```
    rain ALL = NOPASSWD:/sbin/reboot
    ```
    This allows `rain` to run `sudo reboot` without a password, keeping it simple for devops tasks.
  - I didn’t add `rain` to the `sudo` group (which would give full root access) because I wanted limited privileges.

![Edit sudoer file with visudo](/screenshots/day-13/edit-sudoer-file.png)

- **Testing the Setup**:
  - I switched to `rain` with `sudo su rain` and tested his permissions:
    - `df -h` worked fine (no `sudo` needed).
    - `sudo reboot` worked without a password, as configured.
    - Other `sudo` commands (e.g., `sudo less /etc/shadow`) failed, confirming his limited access.
  - I exited with `exit` to return to my main user.

![Test sudo privileges](/screenshots/day-13/test-sudoer-after-config.png)

## Issues Encountered and Solutions

- **Issue: Password Not Prompted**  
  - *Problem*: `adduser` didn’t ask for a password on my system.  
  - *Solution*: I ran `sudo passwd rain` to set it manually. Different Linux distros handle `adduser` slightly differently.

- **Issue: Confusion Between `adduser` and `useradd`**  
  - *Problem*: I saw `useradd` in some tutorials and wasn’t sure which to use.  
  - *Solution*: I learned `adduser` is easier and sets up defaults (like home directories), while `useradd` is more manual. I stuck with `adduser`.

- **Issue: Testing Permissions Without Logging Out**  
  - *Problem*: I didn’t want to log out to test `rain`.  
  - *Solution*: `sudo su rain` let me switch users temporarily and test his commands.

- **Issue: Editing `/etc/sudoers` Safely**  
  - *Problem*: I was worried about breaking the `sudoers` file.  
  - *Solution*: `visudo` checked my syntax automatically, so I couldn’t save a bad file. I added the line for `rain` confidently.

## References

- [Restricting shell access](http://www.cyberciti.biz/tips/howto-linux-shell-restricting-access.html)
- [Learn how to use the $EDITOR environmental variable to set your default editor to `vim`](https://www.a2hosting.com/kb/developer-corner/linux/setting-the-default-text-editor-in-linux)
-  [How To Edit the Sudoers File](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file)

---

**Quick Tip**: Use `visudo` for editing `/etc/sudoers`—it’s a lifesaver if you mistype! This README captures my experience setting up a help-desk user in Linux—hope it’s helpful for your DevOps journey too!
