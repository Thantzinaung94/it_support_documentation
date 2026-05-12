# Home Lab Documentation – Ubuntu SSH Environment

## Project Overview

This home lab project was created to practice Linux server administration, SSH remote access, and basic networking concepts in a virtualized environment.

The lab environment consists of an Ubuntu Server running inside VMware, with remote connections established from both a Windows 11 machine and a separate Linux machine. SSH was configured and tested successfully across both platforms.

### Objectives

- Configure a static IP address on Ubuntu Server
- Enable and configure SSH access
- Allow remote administration from Windows and Linux clients
- Practice secure remote connectivity and troubleshooting

---

# Network Topology

## Environment Summary

| Device | Operating System | Purpose | Connection Method |
|---|---|---|---|
| Ubuntu Server VM | Ubuntu Server | SSH Server | VMware Virtual Network |
| Windows Client | Windows 11 | SSH Client | PuTTY |
| Linux Client | Linux Distribution | SSH Client | Terminal SSH |

---

## Text-Based Network Topology

```text
                    +-------------------+
                    |   Windows 11 PC   |
                    |      (PuTTY)      |
                    +---------+---------+
                              |
                              |
                        SSH Connection
                              |
                              |
+---------------------------------------------------+
|               VMware Virtual Network              |
|                                                   |
|    +-----------------------------------------+    |
|    |          Ubuntu Server VM               |    |
|    |-----------------------------------------|    |
|    | Static IP Configured                    |    |
|    | OpenSSH Server Enabled                  |    |
|    | SSH Root Login Enabled                  |    |
|    +-----------------------------------------+    |
|                                                   |
+---------------------------------------------------+
                              |
                              |
                        SSH Connection
                              |
                              |
                    +---------+---------+
                    |    Linux Client   |
                    |    (Terminal)     |
                    +-------------------+
```

---

# Configuration Steps

## 1. Configure Static IP Address

The Ubuntu Server was assigned a static IP address to ensure consistent connectivity.

### Edit Netplan Configuration

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

### Example Configuration

```yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1
```

### Apply Configuration

```bash
sudo netplan apply
```

### Verify IP Address

```bash
ip a
```

---

## 2. Install OpenSSH Server

### Install SSH Package

```bash
sudo apt update
sudo apt install openssh-server -y
```

### Verify SSH Service Status

```bash
sudo systemctl status ssh
```

---

## 3. Configure SSH Settings

The SSH configuration file was modified to allow root login and enable remote access.

### Open SSH Configuration File

```bash
sudo nano /etc/ssh/sshd_config
```

### Modified Parameters

```text
PermitRootLogin yes
PasswordAuthentication yes
```

> Note: Enabling root login is acceptable for a lab environment but is not recommended in production systems.

---

## 4. Restart SSH Service

After modifying the configuration file, the SSH service was restarted.

```bash
sudo systemctl restart ssh
```

### Verify SSH Service

```bash
sudo systemctl status ssh
```

---

# Verification

## 1. Test Connection from Windows 11

### Tool Used

- PuTTY

### Steps

1. Open PuTTY
2. Enter Ubuntu Server IP address
3. Select SSH connection type
4. Click **Open**
5. Log in using root credentials

### Successful Result

```text
login as: root
root@192.168.1.100's password:
Welcome to Ubuntu Server
```

---

## 2. Test Connection from Linux Client

### Command Used

```bash
ssh root@192.168.1.100
```

### Successful Result

```text
root@ubuntu-server:~#
```

---

## 3. Network Connectivity Test

### Ping Test

```bash
ping 192.168.1.100
```

### Expected Output

```text
64 bytes from 192.168.1.100: icmp_seq=1 ttl=64 time=0.5 ms
```

---

# SSH Hardening Recommendations

Although this lab enabled root login for learning purposes, the following security improvements are recommended:

| Recommendation | Description |
|---|---|
| Disable Root Login | Use a standard user account with sudo privileges |
| Use SSH Keys | Replace password authentication with key-based authentication |
| Change Default SSH Port | Reduce automated scanning attempts |
| Enable Firewall | Restrict unauthorized access |
| Disable Password Authentication | Improve SSH security |

### Example Secure SSH Configuration

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

---

# Troubleshooting

## Common SSH Issues

### 1. SSH Service Not Running

#### Check Service Status

```bash
sudo systemctl status ssh
```

#### Restart Service

```bash
sudo systemctl restart ssh
```

---

### 2. Connection Refused

#### Possible Causes

- SSH service stopped
- Incorrect IP address
- Firewall blocking port 22

#### Verify Listening Port

```bash
sudo ss -tulnp | grep ssh
```

---

### 3. Permission Denied

#### Possible Causes

- Incorrect username/password
- Root login disabled
- Wrong SSH configuration

#### Verify SSH Settings

```bash
sudo nano /etc/ssh/sshd_config
```

Ensure:

```text
PermitRootLogin yes
PasswordAuthentication yes
```

---

### 4. Firewall Blocking SSH

#### Check UFW Status

```bash
sudo ufw status
```

#### Allow SSH

```bash
sudo ufw allow ssh
```

or

```bash
sudo ufw allow 22/tcp
```

---

### 5. Static IP Not Applied

#### Reapply Netplan

```bash
sudo netplan apply
```

#### Validate Configuration

```bash
sudo netplan try
```

---

# Conclusion

This networking home lab successfully demonstrated:

- Ubuntu Server deployment on VMware
- Static IP configuration
- OpenSSH installation and configuration
- Remote SSH access from Windows and Linux systems
- Basic SSH troubleshooting and security practices

The lab provides a strong foundation for learning Linux administration, networking, and remote server management.