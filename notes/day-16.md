# Day 16 - Working with Compressed Archives in Linux

## Objectives

- Learn how to create and manage compressed archives (tarballs) in Linux.  
- Understand the difference between archiving and compressing files.  
- Practice extracting files from tarballs and verify the results.  
- Explore how these skills apply to real-world tasks like backups and software installation. 

## Basic Commands Practiced

| Command            | Description                                           | Usage Example                                      |
|--------------------|-------------------------------------------------------|----------------------------------------------------|
| `tar -cvf`        | Creates an uncompressed archive of files or directories. | `tar -cvf myinits.tar /etc/init.d/`             |
| `gzip`            | Compresses a file using GnuZip.                       | `gzip myinits.tar`                                |
| `tar -cvzf`       | Creates a compressed archive in one step.             | `tar -cvzf myinits.tgz /etc/init.d/`             |
| `tar -xvf`        | Extracts files from an uncompressed archive.          | `tar -xvf myinits.tar`                            |
| `tar -xvzf`       | Extracts files from a compressed archive.             | `tar -xvzf myinits.tgz`                           |
| `cp`              | Copies files or directories to another location.      | `cp myinits.tgz /tmp/`                            |
| `ls -l`           | Lists files with details, such as size.               | `ls -l myinits.tar myinits.tgz`                   |

## Lessons and Notes

- **Archiving vs. Compressing**:  
  - Archiving with `tar` bundles files into one file (e.g., `tar -cvf myinits.tar /etc/init.d/`).  
  - Compression with `gzip` shrinks that file (e.g., `gzip myinits.tar` produces `myinits.tar.gz`).  
  - Using `tar -cvzf` combines both steps, creating a compressed tarball like `myinits.tgz` in one go.  

![Create tar and then gzip it](/screenshots/day-16/create-gzip-file.png)

- **Command Switches Explained**:  
  - `-c`: Create a new archive.  
  - `-v`: Verbose mode (shows what’s happening).  
  - `-z`: Compress with GnuZip.  
  - `-f`: Specify the output file (must come last when creating an archive).  
  - **Key Takeaway**: The order matters—`-f` expects the filename right after it.  

- **Size Matters**:  
  - I made an uncompressed archive (`myinits.tar`) and a compressed one (`myinits.tgz`) of `/etc/init.d/`. Using `ls -l`, I saw the compressed version was much smaller, proving compression’s value.  

![Compare size file .tar and .gz](/screenshots/day-16/compare-size-tar-and-gzip.png)

- **Extracting Files**:  
  - For uncompressed archives: `tar -xvf myinits.tar`.  
  - For compressed tarballs: `tar -xvzf myinits.tgz`.  
  - I tested extraction in `/tmp` after copying the files there with `cp`, keeping my working directory clean.  

![Extracted file myinits](/screenshots/day-16/extract-file-to-tmp.png)

- **Real-World Use**:  
  - Tarballs are everywhere in DevOps—backing up configs, distributing software, or installing from source. Mastering this is a stepping stone to bigger tasks.


## Issues Encountered and Solutions

- **Issue: Switch Order Confusion**  
  - *Problem*: I messed up the order of `-f`, causing `tar` to fail.  
  - *Solution*: Realized `-f` must be the last switch when creating an archive, followed by the filename.  

- **Issue: Where to Extract?**  
  - *Problem*: I didn’t want to clutter my directory while testing extraction.  
  - *Solution*: Copied archives to `/tmp` with `cp` and extracted them there—safe and tidy.  

- **Issue: Silent Commands**  
  - *Problem*: Without `-v`, `tar` ran silently, and I couldn’t tell if it worked.  
  - *Solution*: Added `-v` for verbose output, which showed every file being processed.  

## References

- [18 Tar Command Examples in Linux](https://www.tecmint.com/18-tar-command-examples-in-linux/)
- [Linux TAR Command](http://linuxbasiccommands.wordpress.com/2008/04/04/linux-tar-command/)

