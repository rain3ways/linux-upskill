# Day 9 - Securing a Server with Firewalls and Port Management

## Objectives

- Learn why open ports on a server matter and how they can be potential security risks.
- Practice identifying open ports using tools like `ss` and `nmap`.
- Secure my server by setting up a firewall with `ufw` to control access to services like SSH and HTTP.
- Explore the idea of using non-standard ports (e.g., for SSH) and understand "security by obscurity."

## Basic Commands Practiced

Here are the key commands I used, along with their descriptions and examples:

| Command       | Description                                           | Usage Example                                      |
|---------------|-------------------------------------------------------|----------------------------------------------------|
| `ss -ltpn`    | Shows listening sockets (open ports) and the processes using them. | `sudo ss -ltpn`                          |
| `nmap`        | Scans a target to identify open ports and services.   | `nmap localhost` or `nmap <server_ip>`             |
| `ip a`        | Displays network interfaces and their IP addresses.   | `ip a`                                             |
| `iptables -L` | Lists current firewall rules managed by `iptables`.   | `sudo iptables -L`                                 |
| `ufw allow`   | Permits traffic to a specific port or service.        | `sudo ufw allow ssh`                               |
| `ufw deny`    | Blocks traffic to a specific port or service.         | `sudo ufw deny http`                               |
| `ufw enable`  | Activates the firewall with the configured rules.     | `sudo ufw enable`                                  |

## Lessons and Notes

- **Checking Open Ports**:
  - Using `ss -ltpn`, I saw that my server had ports 22 (SSH) and 80 (HTTP) open to the world (`0.0.0.0:22` and `*:80`), meaning they were accessible externally. Port 53 (DNS) was only on the loopback interface (`127.0.0.53%lo:53`), so it wasn’t exposed.
  - With `nmap localhost`, I confirmed that ports 22 and 80 were open locally. Scanning my server’s external IP (found via `ip a`) showed what’s visible to the outside world.

- **Network Interfaces**:
  - The `ip a` command helped me identify my server’s IP addresses and interfaces (e.g., loopback vs. public-facing). This is key to understanding which services are exposed.

- **Firewall Basics**:
  - Initially, `sudo iptables -L` showed no rules—everything was wide open! The Linux kernel uses `netfilter` for firewalling, but tools like `iptables` are complex, so I used `ufw` instead.
  - I installed `ufw` with `sudo apt install ufw` (it’s standard on Ubuntu) and set rules like `sudo ufw allow ssh` and `sudo ufw deny http`. After enabling it with `sudo ufw enable`, HTTP traffic was blocked, even though Apache was still running locally.

- **Testing and Safety**:
  - After denying HTTP, I tested with a browser and confirmed the web server was inaccessible externally—proof the firewall worked! I reversed it with `sudo ufw allow http` to restore access.
  - **Critical Lesson**: Always allow SSH before enabling the firewall, or you’ll lose access to your server!

- **Security by Obscurity**:
  - Changing SSH from port 22 to something like 2222 (via `/etc/ssh/sshd_config`) can dodge basic attacks. It’s not true security—more like hiding—but it reduces noise from opportunistic hackers. If I did this, I’d need to update firewall rules (and cloud security groups, e.g., AWS EC2) to match.

Overall, I learned that securing a server means minimizing open ports and using a firewall to control access—core DevOps skills!

## Issues Encountered and Solutions

I hit a few bumps along the way, but each taught me something valuable:

- **No `nmap` Installed**:
  - Problem: `nmap` wasn’t on my server by default.
  - Solution: Installed it with `sudo apt install nmap`.

- **Confusing `ss` Output**:
  - Problem: Terms like `0.0.0.0:22` and `127.0.0.53%lo:53` were tricky at first.
  - Solution: Learned that `0.0.0.0` means "all interfaces" (external access), while `127.0.0.1` is local-only.

- **Risk of Locking Myself Out**:
  - Problem: I worried about losing SSH access if I misconfigured the firewall.
  - Solution: Made sure to run `sudo ufw allow ssh` before `sudo ufw enable`.

- **Verifying Firewall Rules**:
  - Problem: Needed to confirm HTTP was blocked externally.
  - Solution: Tested with a browser from another device after denying port 80—worked as expected.

These hiccups emphasized the need for caution and testing when securing a server.

## References
