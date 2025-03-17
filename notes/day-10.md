# Day10 - Scheduling Tasks with `at` and `cron` in Linux

## Objectives

- Understand how to schedule one-time tasks using the `at` command in Linux.
- Learn to use `cron` and `crontab` for recurring task automation.
- Practice automating common system administration tasks, such as backups and cleanup.
- Gain insight into system-wide cron jobs and their differences from user-specific cron jobs.

## Basic Commands Practiced


| Command           | Description                                           | Usage Example                                      |
|-------------------|-------------------------------------------------------|----------------------------------------------------|
| `at`              | Schedules a one-time task to run at a future time.    | `echo 'command' | at now + 1 minute`              |
| `crontab -e`      | Edits the current user's crontab file.                | `crontab -e`                                      |
| `crontab -l`      | Displays the current user's crontab entries.          | `crontab -l`                                      |
| `crontab -r`      | Deletes the current user's crontab.                   | `crontab -r`                                      |
| `tty`             | Shows the terminal file connected to standard input.  | `tty` (e.g., outputs `/dev/pts/0`)                |
| `date`            | Displays the current date and time.                   | `date -I` (e.g., outputs `2024-05-26`)            |
| `tar`             | Creates compressed archives of files/directories.     | `tar -czvf archive.tar.gz /path/to/dir`           |
| `find`            | Searches for files based on specified criteria.       | `find /path -name "pattern" -mtime +7 -delete`    |
| `systemctl list-timers` | Lists active systemd timers.                    | `systemctl list-timers`                           |

## Lessons and Notes

This exercise introduced me to the power of task scheduling in Linux, a fundamental DevOps skill:

- **Using `at` for One-Time Tasks**:
  - I started by installing `at` on Ubuntu with `sudo apt install at`. Then, I scheduled a simple task to echo a greeting to my terminal after 1 minute (e.g., `echo 'echo "Greetings $USER!" > /dev/pts/0' | at now + 1 minute`). It was exciting to see it work!

![at command demo](/screenshots/day-10/at-command-demo.png)

- **Cron and Crontab Basics**:
  - Each user has their own crontab, which I managed using `crontab -e` to edit, `crontab -l` to list, and `crontab -r` to remove. I created a cron job to print "Hello world!" every minute (`* * * * * echo "Hello world!" > /dev/pts/0`), which helped me grasp the syntax:  
    ```
    * * * * * command
    | | | | |
    | | | | +--- Day of week (0-7)
    | | | +----- Month (1-12)
    | | +------- Day of month (1-31)
    | +--------- Hour (0-23)
    +----------- Minute (0-59)
    ```
  - I found [crontab.guru](https://crontab.guru/) super helpful for testing cron expressions.

![Print Hello world with crontab](/screenshots/day-10/crontab-hello-world-demo.png)

- **Automating Backups**:
  - I used `tar` and `date` to create daily backups of `/home`, naming them with the date (e.g., `tar -czvf /var/backups/home.$(date -I).tar.gz /home/`). I scheduled this to run at 5:00 AM daily with `0 5 * * *`.

![Create an auto backup with crontab](/screenshots/day-10/create-crontab-back-up.png)

- **Cleaning Up Old Files**:
  - To manage disk space, I used `find` to delete backups older than 7 days (e.g., `find /var/backups -name "home.*.tar.gz" -mtime +7 -delete`). I scheduled this at 5:30 AM daily with `30 5 * * *`.

![Autom delete old backups with crontab](/screenshots/day-10/crontab-auto-delete-old-backups.png)

- **System-wide Cron Jobs**:
  - The system crontab at `/etc/crontab` includes a user field (e.g., `root`), unlike user crontabs. It also manages scripts in directories like `/etc/cron.daily/`. I learned this is less common now, with user crontabs being preferred.

- **Systemd Timers**:
  - I peeked at `systemctl list-timers` to see an alternative to cron, which I’ll explore further later.

Automating tasks like these saves time and prevents problems—core ideas in DevOps!

## Issues Encountered and Solutions

I hit a few bumps along the way, but solving them was a great learning experience:

- **Issue: `at` Not Installed**  
  - *Problem*: `at` wasn’t available by default on Ubuntu.  
  - *Solution*: Installed it with `sudo apt install at`.

- **Issue: Editor Prompt in `crontab -e`**  
  - *Problem*: First time running `crontab -e`, I had to pick an editor.  
  - *Solution*: Chose `vim.basic` (option 2), but any familiar editor works.

- **Issue: Slow Cron Testing**  
  - *Problem*: Waiting for cron jobs to run at specific times took too long.  
  - *Solution*: Tested with `* * * * *` (every minute), then adjusted to the real schedule.

- **Issue: Permissions for Cron Jobs**  
  - *Problem*: Some commands failed in cron due to insufficient permissions.  
  - *Solution*: For root-level tasks, I used `sudo crontab -e` to edit the root crontab.


## References

- [Arabesque: Cron best practices](https://blog.sanctum.geek.nz/cron-best-practices/)
- [How to Use Systemd Timers as a Cron Replacement](https://www.maketecheasier.com/use-systemd-timers-as-cron-replacement/)
- [nixCraft: How To Add Jobs To cron Under Linux or UNIX](https://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/)
-  [How to Use Systemd Timers as a Cron Replacement](https://www.maketecheasier.com/use-systemd-timers-as-cron-replacement/)