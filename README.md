# SSH Key-Based Authentication on CentOS Stream

A step-by-step guide to configuring SSH key-based authentication on a CentOS Stream server using PuTTY from a Windows client.

This project also demonstrates how to improve SSH security by:

- Generating SSH public/private key pairs
- Configuring key-based authentication
- Disabling password authentication
- Changing the default SSH port
- Updating SELinux configuration
- Configuring FirewallD for the new SSH port

---

## Features

- SSH Key Authentication
- PuTTY & PuTTYgen Configuration
- Password Authentication Disabled
- Custom SSH Port
- SELinux Configuration
- FirewallD Configuration
- Windows Client → Linux Server Connection

---

## Requirements

- CentOS Stream
- Windows
- PuTTY
- PuTTYgen
- SSH Server (sshd)

---

## Project Structure

```
.
├── ssh.pdf
└── README.md
```

---

## Configuration Steps

### Part 1
Generate SSH keys using PuTTYgen and configure key-based authentication.

- Create `.ssh` directory
- Generate Public & Private Keys
- Save private key (.ppk)
- Copy public key to:

```bash
~/.ssh/authorized_keys
```

Set permissions:

```bash
chmod -R 700 ~/.ssh
```

Restart SSH service:

```bash
systemctl restart sshd
```

---

### Part 2
Disable Password Authentication

Edit:

```bash
/etc/ssh/sshd_config
```

Change:

```text
PasswordAuthentication yes
```

to

```text
PasswordAuthentication no
```

Restart SSH:

```bash
systemctl restart sshd
```

---

### Part 3
Change Default SSH Port

Example:

```text
22 → 7500
```

Update SELinux:

```bash
semanage port -a -t ssh_port_t -p tcp 7500
```

Allow the new port through FirewallD:

```bash
firewall-cmd --add-port=7500/tcp --zone=public --permanent
firewall-cmd --reload
```

Verify active zones:

```bash
firewall-cmd --get-active-zones
```

---

## Security Improvements

- Encrypted SSH communication
- Public/Private Key Authentication
- Password Login Disabled
- Custom SSH Port
- SELinux Enforcement
- Firewall Configuration

---

## Technologies

- CentOS Stream
- PuTTY
- PuTTYgen
- SELinux
- FirewallD

---

## Documentation

The full implementation guide is available in:

```
ssh.pdf
```
---

##  Screenshoots

![img](images/ssh(14).png)
![img](images/ssh(16).png)
![img](images/ssh(21).png)
![img](images/ssh(4).png)

##Note 

   prepared as a practical guide for securing SSH access on Linux servers using key-based authentication 


## Author

**Duha Naasan**

System Administrator | Linux Administrator | Windows Server Administrator

- GitHub: https://github.com/DUHA-na
- LinkedIn: https://linkedin.com/in/duha-naasan