

# Day 7- Apache2 Web Server Installation and Configuration

## Objectives
- Install and run Apache2 on a Linux server to transform it into a functional web server.
- Develop skills in installing applications, managing services, editing configuration files, and viewing logs in a Linux environment.
- Practice essential Linux commands for package and service management to deepen my understanding of a DevOps engineer's responsibilities.



## Basic Commands Practiced

| Command                    | Description                                   | Usage Example                    |
|----------------------------|-----------------------------------------------|----------------------------------|
| `sudo apt update`          | Updates the list of available packages from the repository | `sudo apt update`                |
| `sudo apt install apache2` | Installs the Apache2 web server               | `sudo apt install apache2`       |
| `sudo systemctl stop apache2` | Stops the Apache2 service                  | `sudo systemctl stop apache2`    |
| `sudo systemctl start apache2`| Starts the Apache2 service                | `sudo systemctl start apache2`   |
| `systemctl status apache2` | Displays the current status of the Apache2 service | `systemctl status apache2`       |
| `less /etc/apache2/apache2.conf` | Views the primary Apache2 configuration file | `less /etc/apache2/apache2.conf` |
| `sudo vim /var/www/html/index.html` | Edits the default web page        | `sudo vim /var/www/html/index.html` |
| `sudo apt upgrade`         | Upgrades all installed packages to their latest versions | `sudo apt upgrade`               |



## Lessons and Notes

### 1. **Installing Apache2**
- Begin by refreshing the package list to ensure access to the latest software versions:
  ```bash
  sudo apt update
  ```
- Install Apache2 using the following command:
  ```bash
  sudo apt install apache2
  ```
- Confirm that Apache2 is operational by visiting `http://[external IP]` in a browser. Seeing the default Apache page indicates success.

![Checking Default Apache Site](/screenshots/day-7/apache-test.png)

### 2. **Managing the Apache2 Service**
- Apache2 operates as a background service that starts automatically on server boot.
- To stop the service for testing:
  ```bash
  sudo systemctl stop apache2
  ```
  (The web page should become inaccessible.)
- Restart the service:
  ```bash
  sudo systemctl start apache2
  ```
- Check its status:
  ```bash
  systemctl status apache2
  ```
  (This provides detailed feedback, including whether the service is active.)

### 3. **Configuring Apache2**
- The primary configuration file is `/etc/apache2/apache2.conf`. View it with:
  ```bash
  less /etc/apache2/apache2.conf
  ```
- The line `IncludeOptional conf-enabled/*.conf` in this file enables Apache2 to load additional configuration files from the `conf-enabled/` directory, showcasing Linux’s modular configuration style.

### 4. **Editing the Default Web Page**
- The default web page resides at `/var/www/html/index.html`.

![View file index.html](/screenshots/day-7/inside-file-index-html.png)

- Edit it using `vim`:
  ```bash
  sudo vim /var/www/html/index.html
  ```

- I replaced the original content with a simple HTML page sourced from `http://165.227.92.20/sample`, then personalized it. After saving, I refreshed `http://[external IP]` to view the updates.

![Change Default Page Apache](/screenshots/day-7/default-web-edited.png)

### 5. **Viewing Apache2 Logs**
- Logs are located in `/var/log/apache2/`, including:
  - `access.log`: Tracks web page access requests (e.g., my browser visits).
  - `error.log`: Logs any errors (mine was empty, thankfully!).
- Inspect logs with:
  ```bash
  less /var/log/apache2/access.log
  ```

### 6. **Basic Security**
- Installing Apache2 opens port 80, expanding the server’s exposure to potential attacks. To enhance security, I updated the system:
  ```bash
  sudo apt update
  sudo apt upgrade
  ```
  This ensures all packages, including Apache2, have the latest security patches.


## Issues Encountered and Solutions

- **Issue 1**: Unable to access the web page using the public IP.
  - **Solution**: Adjusted the security group (e.g., on AWS, Azure, GCP, or OCI) to allow inbound traffic on port 80.

- **Issue 2**: Lacked permission to modify `index.html`.
  - **Solution**: Used `sudo` for elevated privileges:
    ```bash
    sudo vim /var/www/html/index.html
    ```

- **Issue 3**: Apache2 service failed to run after being stopped.
  - **Solution**: Restarted it with:
    ```bash
    sudo systemctl start apache2
    ```
    Then verified it with:
    ```bash
    systemctl status apache2
    ```



## References
- [HTTPD - Apache2 Web Server](https://documentation.ubuntu.com/server/how-to/web-services/install-apache2/index.html)
- [Using systemctl to manage services](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)

