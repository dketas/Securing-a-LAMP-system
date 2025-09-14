## Securing-a-LAMP-system
"Securing a LAMP System: This project demonstrates the setup and hardening of a Linux VM with LAMP stack and WordPress CMS. It includes VM configuration, system updates, SSH setup, firewall hardening, TLS/HTTPS configuration with Let’s Encrypt, and overall OS and CMS security best practices."

## Table of Contents
# Virtual Machine Creation and Disk Import
- Created a VM with the imported system disk as the sole disk.
- Assigned 2 CPUs and 2 GiB RAM (4 GiB used when host had ≥16 GiB RAM).
- Avoided ISO installation; used existing system disk.

# Root Password Setup and Keyboard Configuration
- Set a new, strong root password for security.
- Adjusted keyboard layout inside VM to match hardware using `localectl`.

# Network Configuration
- Configured the new virtual network card to restore network connectivity.
- Verified network operation and internet access inside the VM.

# System Updates
- Performed system updates using `dnf` with safe options.
- Determined if reboot was needed by checking open deleted files (`lsof` + `grep deleted`), kernel version (`uname -a`), and `/boot` contents.
- Rebooted VM only when necessary.

# SSH Daemon Enablement and Host Key Generation
- Enabled `sshd` service and confirmed it was active.
- Generated new SSH host keys (RSA, ECDSA, ED25519).
- Documented all SSH key fingerprints.
- Configured port forwarding in the hypervisor to allow SSH from host.

# VM Identification and Login
- Verified VM identity using SSH public host keys.
- Logged into VM remotely via SSH.

# Hostname Configuration
- Set the hostname to the fully qualified domain name (FQDN).

# Service and Process Management
- Listed all running processes and enabled services using `ps auxfw`, `systemctl list-units`.
- Disabled unnecessary services (e.g., bluetooth, atd, rpcbind, smartd, sssd) to reduce attack surface.
- Removed unneeded packages including desktop environment and network file sharing tools.
- Used `systemctl enable/disable/stop` and `dnf remove` responsibly.

# Firewall Configuration
- Checked firewall status (`firewalld`) and current rules.
- Allowed only essential ports: SSH, HTTP, HTTPS.
- Removed insecure or unneeded services (e.g., telnet, cockpit).
- Reloaded firewall to apply changes.

# LAMP Stack Installation and CMS Setup
- Installed Apache HTTP server, MariaDB server, PHP, PHP-FPM, and required PHP extensions.
- Configured `php-fpm` integration with Apache.
- Downloaded and installed latest WordPress CMS in Apache web root.
- Set appropriate file and directory ownership and permissions.
- Configured WordPress with secure database credentials and authentication salts.
- Completed initial WordPress setup via web interface.

# HTTPS Configuration with Trusted TLS Certificate
- Installed `certbot` and Apache plugin.
- Obtained and installed Let’s Encrypt SSL/TLS certificate for domain.
- Verified certificate trust and HTTPS access in browsers, including Firefox.
- Set up automatic renewal of certificates using systemd timers.
- Tested TLS configuration using SSL Labs and achieved a high security rating.

# System, Service, and CMS Hardening
- Hardened OS by disabling/removing unnecessary services and software.
- Enforced secure file permissions and ownership.
- Used trusted software sources and official repositories exclusively.
- Ensured secure SSH key management and firewall configuration.
- Documented all security steps and rationales.

---

# Academic Project Note
This project was completed as part of an academic curriculum to provide hands-on learning and practical understanding of Linux system hardening, secure server setup, and web hosting best practices. The LAMP server configuration on a VM demonstrates real-world IT security principles including update management, SSH security, firewall hardening, and TLS encryption with trusted certificates. 
---

# References
- [WordPress](https://wordpress.org)
- [MariaDB](https://mariadb.org)
- [Certbot - Let's Encrypt](https://certbot.eff.org)
- [SSL Labs TLS Test](https://www.ssllabs.com/ssltest/)
- Rocky Linux Documentation
- Linux man pages and official guides (`dnf`, `systemctl`, `firewall-cmd`)

