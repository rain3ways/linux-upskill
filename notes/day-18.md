
# Day 18 - Managing Logs with Logrotate in Linux

## Objectives

- Understand why log management is critical when administering remote servers in Linux.
- Learn how to use the `logrotate` tool to automate log rotation, compression, and retention.
- Practice checking and modifying log rotation settings for the Apache2 service.

## Basic Commands Practiced

| Command                     | Description                                           | Usage Example                     |
|-----------------------------|-------------------------------------------------------|-----------------------------------|
| `ls /var/log`               | List all log files in the main log directory          | `ls /var/log`                     |
| `ls /var/log/apache2`       | List log files specific to Apache2                    | `ls /var/log/apache2`             |
| `cat /etc/logrotate.conf`   | Display the main `logrotate` configuration file       | `cat /etc/logrotate.conf`         |
| `ls /etc/logrotate.d`       | List service-specific `logrotate` configurations      | `ls /etc/logrotate.d`             |
| `nano /etc/logrotate.d/apache2` | Edit the Apache2 logrotate configuration          | `nano /etc/logrotate.d/apache2`   |

## Lessons and Notes

1. **Why Log Management Matters**  
   - Logs are essential for troubleshooting and monitoring server health, but they can quickly fill up disk space if left unchecked.  
   - The `logrotate` tool helps by automating the process of rotating, compressing, and deleting logs, ensuring servers remain efficient.

2. **How Log Rotation Works**  
   - In `/var/log`, you’ll see files like `/var/log/syslog` alongside older, compressed versions (e.g., `/var/log/syslog.1.gz`). This shows logs are being rotated.  
   - Rotation is typically scheduled via `cron`, which runs the `logrotate` script daily from `/etc/cron.daily`.

![File logs](/screenshots/day-18/file-logs-locate.png)

3. **Exploring Logrotate Configuration**  
   - The primary config file is `/etc/logrotate.conf`, but service-specific settings live in `/etc/logrotate.d/`.  
   - For Apache2, check `/etc/logrotate.d/apache2`. A typical configuration looks like this:  
     ```
     /var/log/apache2/*.log {
         weekly
         missingok
         rotate 52
         compress
         delaycompress
         notifempty
         create 640 root adm
     }
     ```  
     - This rotates Apache2 logs weekly, keeps 52 copies, compresses them, and sets proper permissions.

4. **Customizing Logrotate**  
   - You can tweak settings like rotation frequency (e.g., from `weekly` to `daily`) or the number of logs retained (e.g., `rotate 30` for 30 days).  
   - Advanced options include emailing logs or transferring them to another server for analysis.
  
## Issues Encountered and Solutions

- **Issue**: Logs aren’t rotating as expected.  
  **Solution**: Verify that the `logrotate` script is present in `/etc/cron.daily` and check the syntax in `/etc/logrotate.d/apache2` for errors.  
- **Issue**: Disk space is still running low despite rotation.  
  **Solution**: Reduce the `rotate` value to keep fewer logs or ensure compression is enabled with `compress`.

## Tasks Completed

- **Check Apache2 Logs for Severity 3 Errors**:  
  - Ran `grep "Severity 3" /var/log/apache2/error.log` to filter the error log for Severity 3 entries.  

- **Edit Logrotate to Rotate Apache2 Logs Daily**:  
  - Opened `/etc/logrotate.d/apache2` with `nano`.  
  - Changed `weekly` to `daily` and set `rotate 30` to keep 30 days of logs 

![Edit logrotate of apache2](/screenshots/day-18/edit-logrotate-apache2.png)

  - Execute `sudo logrotate -d /etc/logrotate.conf` to test the configuration, and then run `sudo logrotate -f /etc/logrotate.conf` to apply it.

## References

- [The Ultimate Logrotate Command Tutorial](http://www.thegeekstuff.com/2010/07/logrotate-examples/)
- [Use logrotate to Manage Log Files](http://library.linode.com/linux-tools/utilities/logrotate)