# Day8 - Log Analysis with Command-Line Tools

## Objectives

The main goals of this exercise were to:

- Learn how to view and navigate through server log files using command-line tools.
- Understand how to search and filter log data to find specific information.
- Practice combining commands using pipes to refine searches and extract relevant data.
- Learn to redirect command outputs to files for further analysis or sharing.

## Basic Commands Practiced

| Command    | Description                                           | Usage Example                                      |
|------------|-------------------------------------------------------|----------------------------------------------------|
| `cat`      | Displays the entire contents of a file.              | `cat /var/log/apache2/access.log`                  |
| `less`     | Allows viewing a file with navigation (scrolling, searching). | `less /var/log/apache2/access.log`         |
| `tail`     | Displays the last part of a file.                    | `tail /var/log/apache2/access.log`                 |
| `tail -f`  | Follows a file in real-time, showing new lines as they are added. | `tail -f /var/log/apache2/access.log` |
| `grep`     | Searches for lines matching a pattern.               | `grep "authenticating" /var/log/auth.log`          |
| `cut`      | Extracts specific fields from each line.             | `cut -f 10- -d" "`                                 |
| `sort`     | Sorts the input lines.                               | Used in combination with other commands.           |
| `uniq`     | Reports or filters out repeated lines.               | Used after sorting to find unique entries.         |
| `|`        | Pipes the output of one command to another.          | `grep "authenticating" /var/log/auth.log | grep "root"` |
| `>`        | Redirects output to a file.                          | `command > output.txt`                             |

## Lessons and Notes

Through this exercise, I gained valuable insights into handling and analyzing log files on a server:

- **Viewing Logs**: Commands like `cat`, `less`, and `tail` are fundamental for inspecting log files. `cat` outputs the entire file at once, `less` provides scrollable navigation (with handy shortcuts like `gg` to jump to the top and `/` to search), and `tail` shows the most recent entries.
- **Real-time Monitoring**: The `tail -f` command is incredibly useful for watching logs update in real-time, such as monitoring web server access while browsing the site in a browser.

![View auth.log with tail command](/screenshots/day-8/tail-command-auth-log.png)

- **Searching and Filtering**: `grep` is a powerhouse for finding specific patterns in logs. I learned to chain `grep` commands with pipes (e.g., `grep "authenticating" /var/log/auth.log | grep "root"`) to narrow down results, and even use `-v` to exclude matches (e.g., non-root login attempts).

![Find with grep command](/screenshots/day-8/grep-command-demo.png)

- **Extracting Information**: The `cut` command helped me isolate specific parts of log lines, like IP addresses or messages, by specifying delimiters (e.g., space with `-d" "`) and fields (e.g., `-f 10-` for the 10th field onward).

![Practices with cut command](/screenshots/day-8/cut-command-demo.png)

- **Combining Commands**: Piping with `|` allowed me to build powerful command chains, filtering and processing data step-by-step to get exactly what I needed.
- **Redirecting Output**: Using `>`, I could save command outputs to files (e.g., `grep "root" /var/log/auth.log > attackers.txt`), which is great for later analysis or sharing with others.
- **Understanding Log Files**: I explored key logs like `/var/log/auth.log` (authentication events) and `/var/log/apache2/access.log` (web server access), learning their roles in monitoring server activity.

This exercise underscored how critical log analysis is for DevOps tasks like security monitoring and performance troubleshooting, giving me practical skills to tackle these challenges.

## Issues Encountered and Solutions

- **Missing `/var/log/auth.log`**: On my minimal Ubuntu setup, this file didn’t exist because `rsyslog` wasn’t installed. I fixed it by running `sudo apt install rsyslog`, which created the file and started logging authentication events after a short wait.

## References

- [SED onliners](https://edoras.sdsu.edu/doc/sed-oneliners.html)
- [RegExr - a tool to learn, build and test Regular Expressions](https://regexr.com/)
- [explainshell.com - write down a command-line to see the help text that matches each argument](https://explainshell.com/)



