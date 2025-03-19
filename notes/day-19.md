# Day 19 - Exploring the Linux Virtual Filesystem and File Linking

## Objectives

- Understand the role of the Linux Virtual Filesystem (VFS) as an abstraction layer for file operations.
- Learn about inodes and their significance in file storage, permissions, and ownership.
- Gain hands-on experience with creating hard links and symbolic (soft) links to manage files.
## Basic Commands Practiced

| Command       | Description                                           | Usage Example            |
|---------------|-------------------------------------------------------|--------------------------|
| `ls -li`      | Lists files with their inode numbers                  | `ls -li /etc/hosts`      |
| `stat`        | Shows detailed file information, including inode data | `stat /etc/hosts`        |
| `ln`          | Creates a hard link to an existing file               | `ln /etc/passwd link1`   |
| `ln -s`       | Creates a symbolic (soft) link to a file or directory | `ln -s /etc/passwd link2`|
| `cd`          | Changes to the home directory                         | `cd`                     |
| `less` / `cat`| Displays the contents of a file                       | `less link1`             |

## Lessons and Notes

1. **What is the Linux Virtual Filesystem (VFS)?**  
   - The VFS is a layer in Linux that sits above specific filesystems (like ext3, ext4, or btrfs).  
   - It provides a unified way to interact with files, regardless of the underlying filesystem type.  
   - This abstraction makes Linux flexible and capable of supporting multiple filesystems seamlessly.

2. **Inodes: The Core of File Management**  
   - An **inode** (index node) is a data structure that holds metadata about a file, such as:  
     - Permissions (e.g., `-rw-------`)  
     - Ownership (user and group)  
     - Timestamps (access, modification, change)  
     - Location of the file’s data on disk  
   - Use `ls -li` to see a file’s inode number or `stat` for detailed metadata.  
   - Importantly, permissions and ownership are tied to the inode, not the filename. This allows multiple filenames to reference the same inode (via hard links).

![Stat command demo](/screenshots/day-19/stat-command.png)

3. **Hard Links vs. Symbolic Links**  
   - **Hard Links**:  
     - Created with `ln source target` (e.g., `ln /etc/passwd link1`).  
     - Directly reference the same inode as the original file.  
     - Share the same data and metadata (permissions, ownership, etc.).  
     - Limitations: Can’t link to directories or files on different disks.  
     - If the original file is deleted, the data remains accessible via the hard link.  
   - **Symbolic (Soft) Links**:  
     - Created with `ln -s source target` (e.g., `ln -s /etc/passwd link2`).  
     - Reference the filename, not the inode, so they can link to directories or files across disks.  
     - Have their own inode and typically show full permissions (`lrwxrwxrwx`), but the target file’s permissions apply.  
     - If the original file is moved or deleted, the symlink breaks.  

4. **Real-World Examples**  
   - Symbolic links are widely used in Linux, such as in `/etc/rc2.d/` for startup scripts pointing to `/etc/init.d/`.  
   - Hard links are useful when you need multiple filenames to access the same data without duplicating it.

5. **Key Differences**  
   - Hard links point to the inode (physical data); symlinks point to the filename (abstract path).  
   - Hard links are limited to the same disk; symlinks can span disks.  
   - Deleting the original file affects symlinks (breaks them) but not hard links (data persists).

## Issues Encountered and Solutions

- **Issue**: Tried creating a hard link to a directory but got an error.  
  **Solution**: Hard links only work for files. Use `ln -s` for directories instead.  
- **Issue**: Symbolic link stopped working after moving the original file.  
  **Solution**: Symlinks depend on the target’s path. If the file moves, update the symlink or use a hard link for persistence.  
- **Issue**: Confused by symlink permissions showing `lrwxrwxrwx`.  
  **Solution**: The symlink’s permissions are cosmetic; the target file’s permissions determine access.

## Tasks Completed
- **Created a Hard Link**:  
  - Command: `sudo ln /etc/passwd link1`  
  - Verified with `ls -li` to see the same inode number as `/etc/passwd`.

![Create hard link for passwd file](/screenshots/day-19/create-hard-link-for-passwd.png)

- **Created a Symbolic Link**:  
  - Command: `ln -s /etc/passwd link2`  
  - Checked with `ls -li` and saw it pointing to `/etc/passwd`.  

![Create symbolic link for passwd](/screenshots/day-19/create-symbolic-link-for-passwd.png)

- **Created Aliases**:  
  - Although not explicitly shown, I added a shell alias like `alias ll='ls -l'` to streamline commands (stored in `~/.bashrc`).

![Create alias for ls -li command](/screenshots/day-19/create-alias-for-ls-la.png)

## References

- [Hard and soft links](http://linuxgazette.net/105/pitcher.html)
- [Everything You Ever Wanted to Know About inodes on Linux](https://www.howtogeek.com/465350/everything-you-ever-wanted-to-know-about-inodes-on-linux/)