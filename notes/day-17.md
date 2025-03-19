# Day 17 - Installing Software from Source in Linux

## Objectives

- Understand the reasons and scenarios for installing software from source.  
- Master the process of downloading, compiling, and installing a program manually.  
- Compare this method to using package managers like `apt`.  
- Recognize the challenges of managing dependencies and updates outside a package system.  

## Basic Commands Practiced

| Command                   | Description                                           | Usage Example                                      |
|---------------------------|-------------------------------------------------------|----------------------------------------------------|
| `wget`                    | Downloads files from the internet.                    | `wget -v https://nmap.org/dist/nmap-7.70.tar.bz2`  |
| `tar -jxvf`               | Extracts a compressed tarball (bz2 format).           | `tar -jxvf nmap-7.70.tar.bz2`                      |
| `./configure`             | Prepares the software for compilation.                | `./configure`                                      |
| `make`                    | Compiles the source code into an executable.          | `make`                                             |
| `sudo make install`       | Installs the compiled software system-wide.          | `sudo make install`                                |                                   |
| `nmap -V`                 | Displays the version of `nmap`.                       | `/usr/local/bin/nmap -V`                           |

## Lessons and Notes

- **Why Go to the Source?**  
  - Installing from source is useful when you need the latest features or versions not yet available in repositories. For instance, my Ubuntu system had an older `nmap`, but I wanted the latest release from nmap.org.  

- **Setting Up the Environment**:  
  - I installed `build-essential` using `sudo apt install build-essential` to get tools like `gcc`—crucial for compiling source code.  

- **Fetching and Unpacking**:  
  - Downloaded the `nmap` tarball with `wget -v https://nmap.org/dist/nmap-7.95.tar.bz2`.

![Download nmap source](/screenshots/day-17/download-nmap-source.png)

  - Extracted it using `tar -jxvf nmap-7.95.tar.bz2`, which both decompresses and unpacks the archive.  

![Extract nmap with tar](/screenshots/day-17/extract-nmap.png)

- **Building and Installing**:  
  - Ran `./configure` to check my system and configure the build (e.g., processor type, available libraries).

![Run ./configure file](/screenshots/day-17/run-configure-file.png)

  - Compiled the code with `make`, turning it into an executable.

![Compile the code with make command](/screenshots/day-17/make-command.png)

  - Installed it with `sudo make install`, placing `nmap` in `/usr/local/bin`.  

![Install nmap with make command](/screenshots/day-17/install-nmap-with-make-command.png)

- **Path Management**:  
  - My original `nmap` was in `/usr/bin`, but the new one went to `/usr/local/bin`. The `PATH` variable determines which runs by default—`/usr/bin/nmap` took precedence unless I specified `/usr/local/bin/nmap`.  

- **Manual Updates**:  
  - Since I bypassed `apt`, I won’t get automatic updates. For critical tools, I’d need to track new releases or security patches myself—a key consideration for production systems.  

- **Dependencies Made Easy**:  
  - `nmap` has no dependencies, which simplified this task. Most software isn’t so forgiving, and resolving dependencies manually can be a headache.  

This process highlighted the balance between control (custom builds) and convenience (package managers).

## Issues Encountered and Solutions

- **Issue: No Compilers Available**  
  - *Problem*: Compilation failed without `gcc` or related tools.  
  - *Solution*: Installed `build-essential` with `sudo apt install build-essential`.  

- **Issue: Old `nmap` Version Persisted**  
  - *Problem*: Typing `nmap -V` showed the old version after installation.  
  - *Solution*: Used `which nmap` to find it was running from `/usr/bin`. Tested the new one with `/usr/local/bin/nmap -V`.  

- **Issue: `locate` Missed New Files**  
  - *Problem*: `locate bin/nmap` didn’t find the new installation.  
  - *Solution*: Ran `sudo updatedb` to update the file database, then `locate` worked fine.  

- **Issue:`aclocal-1.16` was not found**
  - *Problem*: The main error indicates that `aclocal-1.16` is not found on your system. This is part of the Automake package, which is required to build certain components of **Nmap**, particularly the **libpcre** library
  - *Solution*: Ran `sudo apt update`, then `sudo apt-get install automake autoconf libtool`.

## References

- [The magic behind configure, make, make install](https://thoughtbot.com/blog/the-magic-behind-configure-make-make-install)
- [Installing From Tarballs](https://dev.to/arbitrary/how-to-install-tarball-tar-files-in-linux-33aa)
- [Compiling things on Ubuntu the Easy Way](https://help.ubuntu.com/community/CompilingEasyHowTo)

---

**Final Tip**: Always check the `README` and `INSTALL` files in the source—they’re goldmines for getting things right. 