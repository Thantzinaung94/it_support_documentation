# File Transfer Between Windows and Ubuntu Server Using SCP (WinSCP Lab)

## Objective
This lab demonstrates how to transfer files securely between a Windows client and an Ubuntu Server using the Secure Copy Protocol (SCP) with WinSCP.

---

# Introduction

SCP (Secure Copy Protocol) is a secure method used to transfer files between systems over SSH (Secure Shell).

In this lab:

- Ubuntu Server acts as the remote server
- Windows 11 acts as the client machine
- WinSCP is used as the graphical SCP client application

---

# Lab Environment

| Device | Operating System | Purpose |
|---|---|---|
| Ubuntu Server | Ubuntu Server 24.04 / 26.04 | File Server |
| Windows PC | Windows 11 | Client Machine |
| Application | WinSCP | SCP File Transfer Tool |

---

# Requirements

Before starting, ensure the following:

- Ubuntu Server is running
- SSH service is installed and enabled
- Windows machine can ping the Ubuntu Server
- WinSCP is installed on Windows

---

# Install OpenSSH Server on Ubuntu

## Step 1: Update Repository

```bash
sudo apt update
```

## Step 2: Install OpenSSH Server

```bash
sudo apt install openssh-server -y
```

## Step 3: Check SSH Service Status

```bash
sudo systemctl status ssh
```

Expected result:

```text
active (running)
```

---

# Check Ubuntu Server IP Address

Use the following command:

```bash
ip a
```

Example output:

```text
192.168.100.10
```

This IP address will be used in WinSCP.

---

# Install WinSCP on Windows

Download WinSCP from the official website:

- https://winscp.net

Install using default settings.

---

# Connect Ubuntu Server Using WinSCP

## Step 1: Open WinSCP

Launch WinSCP from Windows.

---

## Step 2: Configure Login Session

Fill the connection information:

| Setting | Value |
|---|---|
| File Protocol | SCP |
| Host Name | Ubuntu Server IP |
| Port Number | 22 |
| User Name | Ubuntu username |
| Password | User password |

Example:

| Setting | Example |
|---|---|
| Host Name | 192.168.100.10 |
| User Name | ubuntu |
| Password | ******** |

---

## Step 3: Login

Click:

```text
Login
```

If a security warning appears, click:

```text
Accept
```

---

# WinSCP Interface Overview

After login:

| Panel | Description |
|---|---|
| Left Panel | Windows local files |
| Right Panel | Ubuntu Server files |

You can drag and drop files between systems.

---

# Transfer File From Windows to Ubuntu Server

## Method 1: Drag and Drop

1. Select a file from the Windows panel
2. Drag it to the Ubuntu Server panel
3. Release the mouse button

The file will upload automatically.

---

## Method 2: Upload Button

1. Select file from Windows panel
2. Click:

```text
Upload
```

3. Choose destination directory
4. Click:

```text
OK
```

---

# Verify Uploaded File on Ubuntu

Open Ubuntu terminal and run:

```bash
ls -lh
```

Example:

```text
test.txt
```

---

# Transfer File From Ubuntu Server to Windows

## Method 1: Drag and Drop

1. Select file from Ubuntu panel
2. Drag it to Windows panel

The file downloads automatically.

---

## Method 2: Download Button

1. Select remote file
2. Click:

```text
Download
```

3. Choose local destination
4. Click:

```text
OK
```

---

# Common SCP Commands (CLI Method)

Although WinSCP provides a GUI, SCP can also be used in terminal.

---

## Copy File From Windows/Linux Client to Ubuntu Server

```bash
scp test.txt user@192.168.100.10:/home/user/
```

---

## Copy File From Ubuntu Server to Client

```bash
scp user@192.168.100.10:/home/user/test.txt .
```

---

# Transfer Directory Using SCP

## Upload Folder

```bash
scp -r project/ user@192.168.100.10:/home/user/
```

## Download Folder

```bash
scp -r user@192.168.100.10:/home/user/project .
```

---

# Useful Linux Commands for Verification

## Show Current Directory

```bash
pwd
```

## List Files

```bash
ls -l
```

## Show File Content

```bash
cat filename.txt
```

## Create Test File

```bash
touch test.txt
```

---

# Troubleshooting

## Problem: Connection Refused

### Solution

Check SSH service:

```bash
sudo systemctl status ssh
```

Start SSH service:

```bash
sudo systemctl start ssh
```

Enable auto-start:

```bash
sudo systemctl enable ssh
```

---

## Problem: Permission Denied

### Solution

Check username and password.

Verify SSH login:

```bash
ssh username@server-ip
```

---

## Problem: Cannot Ping Server

### Solution

Check network configuration:

```bash
ip a
```

Check firewall settings:

```bash
sudo ufw status
```

Allow SSH:

```bash
sudo ufw allow 22
```

---

# Security Notes

- SCP encrypts data using SSH
- Default SCP port is 22
- Avoid enabling root login unless necessary
- Use strong passwords

---

# Verification

Successful transfer is confirmed when:

- File appears on destination system
- File size matches
- File can be opened successfully

---

# Conclusion

In this lab, secure file transfer between Windows and Ubuntu Server was successfully performed using SCP and WinSCP.

The lab covered:

- Installing SSH service
- Connecting with WinSCP
- Uploading files
- Downloading files
- Using SCP command line
- Basic troubleshooting

This method provides a secure and reliable way to transfer files across systems in a network environment.