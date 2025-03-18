# Day 14 - Linux File Permissions and Ownership

## Objectives

- Grasp the fundamentals of file ownership and permissions in Linux.  
- Learn how to modify file ownership using `chown` and `chgrp`.  
- Practice adjusting file permissions with `chmod` to manage access.  
- Understand how these concepts impact file access for users, groups, and others.  

## Basic Commands Practiced

| Command            | Description                                           | Usage Example                                      |
|--------------------|-------------------------------------------------------|----------------------------------------------------|
| `ls -l`            | Displays detailed file info, including permissions and ownership. | `ls -l tuesday.txt` |
| `chown`            | Changes the user ownership of a file.                 | `sudo chown root tuesday.txt`                     |
| `chown user:group` | Updates both user and group ownership of a file.      | `sudo chown ubuntu:staff tuesday.txt`             |
| `chgrp`            | Changes the group ownership of a file.                | `sudo chgrp ubuntu tuesday.txt`                   |
| `chmod`            | Alters file permissions using symbolic notation.      | `chmod u-w tuesday.txt` (removes user write permission) |
| `cat`              | Shows the contents of a file.                         | `cat tuesday.txt`                                 |
| `vim` or `nano`    | Edits a file (used to test write permissions).        | `vim tuesday.txt`                                 |

## Lessons and Notes

- **File Ownership**:  
  - Every Linux file has a user owner and a group owner. For example, running `ls -l` might show:  
    ```
    -rw-rw-r-- 1 steve staff 4478979 Feb 6 2011 press.txt
    ```
    Here, `steve` owns the file, and `staff` is the group. Anyone else is considered "other."  
  - I practiced changing ownership:  
    - `sudo chown root tuesday.txt` transfers ownership to the `root` user.  
    - `sudo chgrp ubuntu tuesday.txt` assigns the `devops` group as the owner.  

![Change owner and group of tuesday.txt file](/screenshots/day-14/change-owner-and-group-of-file.png)

- **Permissions (Symbolic Notation)**:  
  - Permissions are split into three categories: User (U), Group (G), and Others (O), with possible Read (r), Write (w), and Execute (x) rights.  
  - Examples:  
    - `-rw-r--r--`: User can read/write, group and others can only read.  
    - `-rwxr-xr-x`: User has full access, group and others can read/execute.  
  - I created `tuesday.txt` and modified its permissions:  
    - `chmod u-w tuesday.txt` removed write access for the user.  
    - `chmod o-r tuesday.txt` removed read access for others.  
    - Result: `-r--r-----` (only user and group can read, no write access).  

![Remove permissions with chmod](/screenshots/day-14/remove-permissions-with-chmod.png)

- **Testing Permissions**:  
  - After removing write permissions, I tested editing `tuesday.txt` with `vim`. I could edit but couldn’t save unless I forced it with `:w!` (as the owner). This taught me that ownership can sometimes bypass permissions.  

![Test owner permissions over chmod](/screenshots/day-14/test-owner-permission-over-chmod.png)

  - I restored write access with `chmod u+w tuesday.txt` to edit normally again.  

## Issues Encountered and Solutions

- **Issue: Testing as Another User**  
  - *Problem*: I couldn’t easily test permissions for "others" without switching accounts.  
  - *Solution*: I used `sudo su otheruser` to switch users and check access.  

- **Issue: Owner Overriding Permissions**  
  - *Problem*: As the owner, I could force-save changes in `vim` with `:w!` despite removing write permissions.  
  - *Solution*: I learned owners have elevated privileges, explaining this behavior.  
## References

- [File permissions and attributes](https://wiki.archlinux.org/title/File_permissions_and_attributes)
- [chmod Tutorial](http://catcode.com/teachmod/)
- [What is “umask” and how does it work?](https://askubuntu.com/questions/44542/what-is-umask-and-how-does-it-work)


---

**Pro Tip**: Run `ls -l` often to confirm your changes—it’s a quick way to see permissions and ownership in action.
