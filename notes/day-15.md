# Day 15 - Managing Software Repositories and Packages in Linux

## Objectives

- Learn how the `apt` package manager works behind the scenes in Ubuntu.  
- Figure out how to add and remove software repositories to expand package options.  
- Discover how to find and install software from various sources.  
- Explore installing software without relying on `apt`.  
## Basic Commands Practiced

| Command                   | Description                                           | Usage Example                                      |
|---------------------------|-------------------------------------------------------|----------------------------------------------------|
| `apt install`             | Installs a package from configured repositories.      | `sudo apt install netperf`                         |
| `apt update`              | Refreshes the local list of available packages.       | `sudo apt update`                                  |
| `apt-cache dump`          | Shows all packages available in the repositories.     | `apt-cache dump`                                   |
| `apt-cache show`          | Provides detailed info about a specific package.      | `apt-cache show neofetch`                          |
| `add-apt-repository`      | Adds a new repository (e.g., a PPA) to the system.    | `sudo add-apt-repository ppa:ubuntusway-dev/dev`   |
| `wc -l`                   | Counts lines in command output.                       | `apt-cache dump \| grep "Package:" \| wc -l`       |
| `less`                    | Views file contents interactively.                    | `less /etc/apt/sources.list`                       |

## Lessons and Notes

- **Repositories and Stability**:  
  - Each Linux version (e.g., Ubuntu 18.04) locks in specific software versions for stability. For instance, Ubuntu 18.04 ships with Apache 2.4.29, and `apt` will install that version years later unless you add a newer source. Security updates are backported to maintain safety without changing the version.  
  - I peeked at my repository config in `/etc/apt/sources.list.d/ubuntu.sources` using `less` and saw URLs pointing to Ubuntu’s official repositories.  

![Sources list](/screenshots/day-15/source-list.png)

- **Expanding with Extra Repositories**:  
  - The default repositories offer tons of software (over 30,000 packages in Ubuntu!), but some tools are missing due to stability or licensing constraints.  
  - I enabled the "Multiverse" repository (which includes "non-free" software) by `sudo add-apt-repository multiverse`, then ran `sudo apt update`. This let me install `netperf`, a network performance tool, with `sudo apt install netperf`.

![Enable Multiverse repository](/screenshots/day-15/enable-multiverse-repository.png)

- **Personal Package Archives (PPAs)**:  
  - PPAs are developer-hosted repositories for the latest software. I added one for `neofetch` (a system info tool) using `sudo add-apt-repository ppa:ubuntusway-dev/dev`, updated with `sudo apt update`, and installed it with `sudo apt install neofetch`. 

![Install Neofetch with PPAs](/screenshots/day-15/install-package-from-ppa.png)

  - I checked its version with `neofetch --version` and saw it was newer than the default. PPAs are great for cutting-edge updates but can be unstable due to frequent changes.
  - To remove the repository, run `sudo add-apt-repository --remove ppa:ubuntusway-dev/dev`. Then update your package lists with `sudo apt update`. Next, reinstall Neofetch using `sudo apt install neofetch`. Finally, check the version by executing `neofetch --version` You should notice that the version now differs from what was installed before removing the developer's Neofetch PPA.

![Remove developer's Neofetch PPA](/screenshots/day-15/remove-repository.png)

- **Beyond `apt`**:  
  - I didn’t install anything manually this time, but I learned you can compile software from source if it’s not in a repository. It’s trickier and riskier, but it’s an option for rare cases.  

## Issues Encountered and Solutions

- **Issue: Why Older Versions?**  
  - *Problem*: I didn’t get why Ubuntu uses outdated software versions.  
  - *Solution*: It’s about stability—long-term support (LTS) releases prioritize reliability over new features, with security fixes backported to older versions.  

- **Issue: Tracking Package Origins**  
  - *Problem*: I wanted to know where a package was sourced from.  
  - *Solution*: `apt-cache show <package>` revealed the repository details, giving me clarity.  

## References

- [How to use yum - Introduction](http://fedoranews.org/tchung/howto/2003-11-09-yum-intro.shtml)
- [Package management with APT](https://help.ubuntu.com/community/AptGet/Howto)

---

**Pro Tip**: Always run `sudo apt update` after modifying repositories to sync your package list. 