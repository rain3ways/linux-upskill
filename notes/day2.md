# Day 2 - Linux Upskill Challenge

## Objectives

- Get familiar with using manual pages.
- Practice basic commands for navigating and managing directories and files.

## Manual Page Commands

| Command                  | Description                                                         | Usage Example          |
|--------------------------|---------------------------------------------------------------------|------------------------|
| **man**                  | Displays the manual page for commands.                              | `man cat`              |
| **tldr**                 | Simplifies man pages by providing practical examples.               | `tldr tar`             |
| **apropos** or **man -k**  | Searches for commands based on keywords or descriptions.            | `man -k "remove file"`  |
| **help <command>**       | Provides help for built-in commands if `man` is not available.        | `help export`          |
| **type <command>**       | Checks if a command is built-in and shows its type.                   | `type export`          |
| **info <command>**       | Reads documentation stored in info format.                          | `info ls`              |

![tldr Command Demo](/screenshots/day-2/tldr-command-demo.png)

## Navigating the File Structure

| Command    | Description                                    | Usage Example                |
|------------|------------------------------------------------|------------------------------|
| **man hier**  | Displays a description of the filesystem hierarchy. | `man hier`                 |
| **cd**     | Changes the current directory to the specified path. | `cd /path/to/directory`      |
| **cd ..**  | Moves up one directory level.                  | `cd ..`                      |
| **pwd**    | Prints the current working directory.          | `pwd`                        |

![man hier Command Demo](/screenshots/day-2/man-hier-demo.png)

## Basic Directory Manipulation

| Command              | Description                          | Usage Example       |
|----------------------|--------------------------------------|---------------------|
| **mkdir**            | Creates a new directory.             | `mkdir test`        |
| **rmdir**            | Removes an empty directory.          | `rmdir test`        |
| **rm -r <directory>**| Recursively removes a directory and its contents. | `rm -r test`         |

## Basic File Manipulation

| Command   | Description                 | Usage Example                         |
|-----------|-----------------------------|---------------------------------------|
| **touch** | Creates a new file.         | `touch test.txt`                      |
| **mv**    | Moves or renames a file.    | `mv test.txt /path/to/directory`      |
| **rm**    | Deletes a file.             | `rm test.txt`                         |

## Lessons and Notes

- The **tldr** command is especially useful for beginners when you haven't memorized all the options or command syntax—it provides concise examples and explanations.
- The **man -k** command is very handy when you can’t remember the exact command; you can search using keywords or descriptions.
- The **man hier** command gives a detailed overview of the system's directory structure, which is essential for understanding where key configuration files and logs are stored.
- Remember: **`cd -`** takes you back to the last visited directory.
