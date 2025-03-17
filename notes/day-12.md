# Day 12 - File Transfer with SFTP

## Objectives

As someone new to DevOps, I set out to achieve the following goals in this exercise:

- Understand how to securely transfer files between my local machine and a server using SFTP.
- Practice uploading and downloading files to and from the server.
- Explore how to manage files on the server, including creating directories and handling permissions.
- Learn why SFTP is a practical choice for file transfers in a DevOps workflow.

## Basic Commands Practiced

While this exercise leaned heavily on graphical SFTP clients, I still used a couple of command-line tools to assist with the process:

| Command       | Description                                           | Usage Example                                      |
|---------------|-------------------------------------------------------|----------------------------------------------------|
| `ssh`         | Connects to the server to check or manage files.      | `ssh username@server-ip`                           |
| `sudo`        | Grants elevated privileges to move files on the server. | `sudo mv /home/username/images /var/www/`        |

For the actual file transfers, I relied on graphical SFTP clients like **WinSCP** (Windows) and **CyberDuck** (macOS), which made the process more intuitive with drag-and-drop functionality.

## Lessons and Notes

This exercise introduced me to key concepts about file transfers in a DevOps context. Here’s what I learned:

- **Why Use SFTP?**  
  SFTP (SSH File Transfer Protocol) is a standout choice for moving files because:
  - It runs over SSH (port 22), requiring no additional server setup.
  - It encrypts both data and commands, ensuring top-notch security.
  - It lets you browse the server’s directory structure and manage files easily.
  - It works reliably across networks, even those with strict firewalls (like at work or a café).

- **Comparing Protocols**  
  Other options like SMB, AFP, FTP, and rsync exist, but SFTP wins for its simplicity and security:
  - Unlike FTP, which sends passwords in plain text (a major risk), SFTP keeps everything encrypted.
  - Protocols like SMB or AFP are better for local networks, not remote servers.
  - Setting up alternatives often means more configuration and potential security risks.

- **Setting Up an SFTP Client**  
  I used **WinSCP** on Windows (or **CyberDuck** on macOS) and found the setup simple:
  - **Server**: Entered my server’s IP address.
  - **Port**: Used 22 (default for SSH/SFTP).
  - **Protocol**: Selected SFTP.
  - **Credentials**: Logged in with my server username and password.  
  After connecting, I could see the server’s files and transfer them with ease.

![Login SFTP](/screenshots/day-12/sftp-login.png)

- **File Transfer Practice**  
  - **Downloading**: I grabbed files from my server’s home directory (`/home/username`) and logs from `/var/log` to my local machine.
  - **Uploading**: I created an `images` folder in my home directory on the server and uploaded some photos from my desktop.

![Upload image](/screenshots/day-12/copy-file.png)

  - **Permissions**: I tried creating an `images` folder in the root directory (`/`) but got a “permission denied” error. This taught me that regular users are restricted to their home directories unless they use `sudo`.

![Fail to create directory](/screenshots/day-12/fail-to-create-directory-in-root.png)

- **Managing Files**  
  After uploading files to my home directory, I logged in via `ssh` and used `sudo` to move them to restricted areas like `/var/www/` (e.g., for a web page). This showed me how permissions and privileges work together in Linux.

SFTP proved to be a straightforward and secure way to handle file transfers, making it a valuable tool for DevOps tasks.

## References

- **SFTP Clients**:
  - [WinSCP](https://winscp.net/) (Windows)
  - [CyberDuck](https://cyberduck.io/) (macOS)
  - [FileZilla](https://filezilla-project.org/) (Cross-platform)
- **Guides**:
  - DigitalOcean’s [SFTP Tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server)
  - Ubuntu’s [SSH/SFTP Documentation](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

---

**Quick Tip**: If you’re just starting with SFTP, try transferring a small file first and use `ssh` to double-check its location. It’s a simple way to get comfortable before tackling bigger tasks. This README reflects my first steps into secure file transfers—hopefully, it’s useful for your DevOps journey too!
