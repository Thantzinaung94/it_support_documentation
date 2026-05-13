# Samba File Share Configuration on Ubuntu Server

## Objective
This document explains how to install, configure, and manage a Samba file sharing service on Ubuntu Server. Samba allows Linux systems to share files and folders with Windows and Linux clients over a network using the SMB/CIFS protocol.

---

# Environment

| Component | Details |
|---|---|
| Server OS | Ubuntu Server 24.04 / 26.04 |
| Client OS | Windows 11 / Linux |
| Service | Samba |
| Protocol | SMB/CIFS |
| Network Type | LAN / VMware Network |

---

# What is Samba?

Samba is an open-source software package that provides file and printer sharing services between Linux and Windows systems.

Using Samba, you can:
- Share folders from Ubuntu to Windows
- Access shared folders from Linux
- Create authenticated file sharing
- Manage permissions and user access

---

# Install Samba

Update package lists:

```bash
sudo apt update
```

Install Samba:

```bash
sudo apt install samba -y
```

Verify installation:

```bash
smbd --version
```

Example output:

```bash
Version 4.x.x-Ubuntu
```

---

# Check Samba Service Status

Check service status:

```bash
sudo systemctl status smbd
```

Start Samba service:

```bash
sudo systemctl start smbd
```

Enable Samba at boot:

```bash
sudo systemctl enable smbd
```

Restart Samba service:

```bash
sudo systemctl restart smbd
```

---

# Create Shared Directory

Create a folder for sharing:

```bash
sudo mkdir -p /srv/samba/shared
```

Set permissions:

```bash
sudo chmod 777 /srv/samba/shared
```

> **Note:**  
> `777` gives full permissions to all users.  
> Use carefully in production environments.

---

# Backup Samba Configuration File

Before editing Samba configuration:

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
```

---

# Configure Samba Share

Open Samba configuration file:

```bash
sudo nano /etc/samba/smb.conf
```

Add the following at the bottom of the file:

```ini
[SharedFolder]
   path = /srv/samba/shared
   browseable = yes
   writable = yes
   guest ok = yes
   read only = no
   create mask = 0777
   directory mask = 0777
```

---

# Explanation of Configuration

| Parameter | Description |
|---|---|
| `[SharedFolder]` | Share name visible on network |
| `path` | Directory path to share |
| `browseable` | Allow folder visibility |
| `writable` | Allow writing files |
| `guest ok` | Allow guest access |
| `read only` | Disable read-only mode |
| `create mask` | File permission mask |
| `directory mask` | Folder permission mask |

---

# Test Samba Configuration

Check configuration syntax:

```bash
testparm
```

If configuration is correct, output should show:

```bash
Loaded services file OK.
```

---

# Restart Samba Service

Apply configuration changes:

```bash
sudo systemctl restart smbd
```

---

# Allow Samba Through Firewall

If UFW firewall is enabled:

```bash
sudo ufw allow samba
```

Check firewall status:

```bash
sudo ufw status
```

---

# Create Samba User (Authenticated Access)

Create Linux user:

```bash
sudo adduser sambauser
```

Add Samba password:

```bash
sudo smbpasswd -a sambauser
```

Enable Samba user:

```bash
sudo smbpasswd -e sambauser
```

---

# Secure Samba Share with Authentication

Edit Samba configuration:

```bash
sudo nano /etc/samba/smb.conf
```

Example secure share:

```ini
[SecureShare]
   path = /srv/samba/shared
   valid users = sambauser
   browseable = yes
   writable = yes
   guest ok = no
   read only = no
```

Restart Samba:

```bash
sudo systemctl restart smbd
```

---

# Access Samba Share from Windows

## Method 1 — Using File Explorer

Open File Explorer and type:

```text
\\SERVER-IP\SharedFolder
```

Example:

```text
\\192.168.1.100\SharedFolder
```

---

## Method 2 — Map Network Drive

1. Open **This PC**
2. Click **Map Network Drive**
3. Enter:

```text
\\SERVER-IP\SharedFolder
```

4. Enter Samba username and password if required

---

# Access Samba Share from Linux

Install Samba client:

```bash
sudo apt install smbclient -y
```

List shares:

```bash
smbclient -L //SERVER-IP -U sambauser
```

Connect to share:

```bash
smbclient //SERVER-IP/SharedFolder -U sambauser
```

---

# Common Samba Commands

| Command | Description |
|---|---|
| `testparm` | Check Samba configuration |
| `sudo systemctl restart smbd` | Restart Samba |
| `sudo smbpasswd -a user` | Add Samba user |
| `sudo smbpasswd -x user` | Remove Samba user |
| `smbclient -L` | List available shares |

---

# Troubleshooting

## 1. Cannot Access Shared Folder

Check Samba service:

```bash
sudo systemctl status smbd
```

Check firewall:

```bash
sudo ufw status
```

Verify network connectivity:

```bash
ping SERVER-IP
```

---

## 2. Permission Denied

Fix ownership:

```bash
sudo chown -R nobody:nogroup /srv/samba/shared
```

Fix permissions:

```bash
sudo chmod -R 777 /srv/samba/shared
```

---

## 3. Configuration Error

Validate configuration:

```bash
testparm
```

---

# Verification

## Verify Share Availability

From Windows:

```text
\\SERVER-IP
```

Expected result:
- Shared folder appears
- Files can be uploaded/downloaded

---

# Conclusion

In this lab:
- Samba was installed on Ubuntu Server
- Shared directories were created
- Guest and authenticated shares were configured
- Windows and Linux clients successfully accessed shared folders
- Basic troubleshooting and permission management were tested

Samba provides an efficient way to share files between Linux and Windows systems in both home and enterprise environments.