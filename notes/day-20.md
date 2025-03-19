# Day 20 - Automating Tasks with Shell Scripts

## Objectives

- Grasp the significance of automation in system administration to streamline repetitive tasks.
- Learn the fundamentals of writing shell scripts to manage and automate system operations.
- Develop a script to identify and list the top 3 IP addresses attempting to log into the server.

## Basic Commands Practiced

| Command | Description | Usage Example |
|---------|-------------|---------------|
| `vim`   | Text editor used to create and modify shell scripts | `vim topattack` |
| `chmod` | Modify file permissions to make scripts executable | `chmod +x topattack` |
| `mv`    | Move scripts to a directory in the PATH for easy access | `sudo mv topattack /usr/local/bin/` |
| `grep`  | Filter specific patterns from files, such as log entries | `grep 'Disconnected from' /var/log/auth.log` |
| `cut`   | Extract specific fields from lines of text | `cut -d' ' -f7` |
| `sort`  | Sort lines of text, often used with `uniq` | `sort` |
| `uniq`  | Count unique occurrences of lines | `uniq -c` |
| `head`  | Display the first few lines of output | `head -n 3` |
| `echo`  | Output text to the terminal | `echo "Top attackers:"` |
| `cat`   | Concatenate and display content, useful with here documents | `cat << EOF` |

## Lessons and Notes

1. **Why Shell Scripts Matter**  
   - Shell scripts are sequences of commands stored in text files, executed by the shell (typically `bash` in Linux).
   - They save time, reduce errors, and enable automation of repetitive tasks like log analysis.
   - Scripts can accept parameters and be scheduled (e.g., via `cron`) for regular execution.

2. **Script Creation Basics**  
   - Every script begins with a shebang (`#!/bin/bash` or `#!/usr/bin/env bash`) to specify the interpreter.
   - Use `chmod +x` to make the script executable and run it with `./scriptname` or by placing it in a PATH directory like `/usr/local/bin`.

![Start with Shebang](/screenshots/day-20/hello-world-script.png)

   - Comments (starting with `#`) improve readability and are a good habit.

3. **First Script: `attacker`**  
   - A simple script to extract the IP address of the last failed login attempt from `/var/log/auth.log`.
   - Example: `grep -i "disconnected from" /var/log/auth.log | tail -1 | awk "{print \$8}"`.
   - Key takeaway: Chain commands to process data efficiently.

![Simple script to find attacker](/screenshots/day-20/simple-script-to-find-attacker.png)

4. **Advanced Script: `topattack`**  
   - An extended script that lists the top N attackers based on a parameter (e.g., `./topattack 3`).
   - Features parameter validation, error checking (e.g., log file readability), and formatted output using a here document.
   - Command pipeline: `grep ... | cut ... | sort | uniq -c | sort -nr | head -n "$1"`.

![Upgrade script to find top N attack](/screenshots/day-20/upgrade-script-attack.png)

5. **Beyond Basics**  
   - Sourcing (`source scriptname`) vs. executing (`./scriptname`) affects variable scope.
   - Long pipelines can be split across lines with `\` for clarity.
   - Automation frameworks like Ansible, CloudInit, or Terraform offer advanced scripting options worth exploring.

## Issues Encountered and Solutions

- **Issue**: Script fails with "permission denied."  
  **Solution**: Run `chmod +x scriptname` to grant execute permissions.
- **Issue**: Typing `scriptname` doesn’t work without `./`.  
  **Solution**: Move the script to `/usr/local/bin` with `sudo mv scriptname /usr/local/bin/` or use `./scriptname`.
- **Issue**: No output because `/var/log/auth.log` is inaccessible.  
  **Solution**: Verify file permissions (`ls -l /var/log/auth.log`) and run with `sudo` if needed.
- **Issue**: Incorrect IP extraction due to log format changes.  
  **Solution**: Adjust `grep` and `awk` parameters to match the log structure (e.g., field numbers).

## References

- [Bash scripting tutorial](http://linuxconfig.org/Bash_scripting_Tutorial)
- [BASH Programming - Introduction HOW-TO](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)
- [How to be a good (and lazy) System Administrator](http://www.linuxjournal.com/content/how-be-good-and-lazy-system-administrator)