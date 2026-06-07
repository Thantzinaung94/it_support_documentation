# Linux Mint 22.3 Cinnamon (64-bit) Installation Hands-On Lab

## Overview

This hands-on lab demonstrates how to deploy and configure Linux Mint 22.3 Cinnamon (64-bit) on Microsoft Hyper-V.

---

# Lab Information

| Item                    | Value                            |
| ----------------------- | -------------------------------- |
| Operating System        | Linux Mint 22.3 Cinnamon 64-bit  |
| Virtualization Platform | Microsoft Hyper-V                |
| Virtual Machine Name    | linux-mint                       |
| Computer Name           | linux-mint                       |
| Username                | thantzinaung                     |
| RAM                     | 4 GB                             |
| Storage                 | 50 GB                            |
| Network                 | Default Switch / External Switch |
| Installation Type       | Clean Installation               |

---

# Lab Objectives

By the end of this lab, you will be able to:

* Create a Hyper-V virtual machine
* Install Linux Mint 22.3 Cinnamon
* Configure user account settings
* Verify network connectivity
* Update the operating system
* Perform basic Linux administration tasks

---

# Prerequisites

Before starting, ensure:

* Windows 10/11 Pro, Enterprise, or Windows Server
* Hyper-V Feature Enabled
* Linux Mint 22.3 Cinnamon ISO downloaded
* At least 60 GB free disk space
* Minimum 8 GB host RAM

---

# Step 1: Download Linux Mint 22.3 ISO

Visit the official Linux Mint website:

https://linuxmint.com/download.php

Download:

* Linux Mint 22.3 Cinnamon Edition (64-bit)

Save the ISO file to your local machine.

---

# Step 2: Open Hyper-V Manager

1. Open Start Menu
2. Search:

```
Hyper-V Manager
```

3. Launch Hyper-V Manager

---

# Step 3: Create a New Virtual Machine

Select:

```
Action
 └── New
      └── Virtual Machine
```

---

## Specify Name and Location

Virtual Machine Name:

```text
linux-mint
```

Click **Next**

---

## Specify Generation

Select:

```text
Generation 2
```

Click **Next**

---

## Assign Memory

Startup Memory:

```text
4096 MB
```

Enable:

```text
Use Dynamic Memory
```

(Optional)

Click **Next**

---

## Configure Networking

Select:

```text
Default Switch
```

or

```text
External Virtual Switch
```

Click **Next**

---

## Connect Virtual Hard Disk

Create a virtual hard disk:

```text
Name: linux-mint.vhdx
Size: 50 GB
```

Click **Next**

---

## Installation Options

Select:

```text
Install an operating system from a bootable image file
```

Browse and select:

```text
linuxmint-22.3-cinnamon-64bit.iso
```

Click **Next**

---

## Complete Wizard

Review settings and click:

```text
Finish
```

---

# Step 4: Configure VM Settings

Right-click:

```text
linux-mint
```

Select:

```text
Settings
```

Verify:

### Memory

```text
4096 MB
```

### Processor

```text
2 Virtual Processors
```

### Secure Boot

If installation fails:

```text
Security
 └── Disable Secure Boot
```

Apply changes.

---

# Step 5: Start Virtual Machine

Select:

```text
linux-mint
```

Click:

```text
Start
```

Then:

```text
Connect
```

The Linux Mint installer will boot.

---

# Step 6: Launch Installer

From desktop:

```text
Install Linux Mint
```

Double-click installer.

---

# Step 7: Choose Language

Select:

```text
English
```

Click:

```text
Continue
```

---

# Step 8: Keyboard Layout

Select:

```text
English (US)
```

Click:

```text
Continue
```

---

# Step 9: Multimedia Codecs

Check:

```text
Install Multimedia Codecs
```

Click:

```text
Continue
```

---

# Step 10: Installation Type

Select:

```text
Erase disk and install Linux Mint
```

Since this is a new virtual machine, only the virtual disk will be modified.

Click:

```text
Install Now
```

Confirm:

```text
Continue
```

---

# Step 11: Time Zone

Choose:

```text
Yangon
```

Click:

```text
Continue
```

---

# Step 12: Create User Account

Computer Name:

```text
linux-mint
```

Username:

```text
thantzinaung
```

Your Name:

```text
Thant Zinaung
```

Password:

```text
********
```

Select:

```text
Require my password to log in
```

Click:

```text
Continue
```

---

# Step 13: Reboot System

When prompted:

```text
Restart Now
```

Remove ISO if necessary.

System reboots into Linux Mint.

---

# Step 14: Login

Username:

```text
thantzinaung
```

Password:

```text
********
```

Login to Cinnamon Desktop.

---

# Step 15: Verify System Information

Open Terminal.

Run:

```bash
hostnamectl
```

Expected Output:

```text
Static hostname: linux-mint
Operating System: Linux Mint 22.3
Architecture: x86-64
```

---

# Step 16: Verify Network Connectivity

Check IP Address:

```bash
ip a
```

Test Internet Access:

```bash
ping google.com
```

Expected:

```text
64 bytes from ...
```

Press:

```bash
Ctrl + C
```

to stop.

---

# Step 17: Update Linux Mint

Update package list:

```bash
sudo apt update
```

Upgrade packages:

```bash
sudo apt upgrade -y
```

Clean unused packages:

```bash
sudo apt autoremove -y
```

---

# Step 18: Useful Linux Commands

## Current User

```bash
whoami
```

---

## Current Directory

```bash
pwd
```

---

## List Files

```bash
ls -la
```

---

## System Information

```bash
uname -a
```

---

## Memory Usage

```bash
free -h
```

---

## Disk Usage

```bash
df -h
```

---

## CPU Information

```bash
lscpu
```

---

## Network Interfaces

```bash
ip addr
```

---

## Running Processes

```bash
top
```

Quit:

```text
q
```
---

# Lab Validation Checklist

| Task                     | Status |
| ------------------------ | ------ |
| VM Created               | ✓      |
| Linux Mint Installed     | ✓      |
| Hostname Configured      | ✓      |
| User Created             | ✓      |
| Network Working          | ✓      |
| Internet Access Verified | ✓      |
| System Updated           | ✓      |
| Basic Commands Tested    | ✓      |

---

![MintLinux22.3Installation](./asset/image/MintLinux22.3Installation.png)
![01](./asset/image/01.jpg)
![02](./asset/image/02.jpg)
![03](./asset/image/03.jpg)
![04](./asset/image/04.jpg)
![05](./asset/image/05.jpg)
![06](./asset/image/06.jpg)
![07](./asset/image/07.jpg)
![08](./asset/image/08.jpg)
![09](./asset/image/09.jpg)
![10](./asset/image/10.jpg)
![11](./asset/image/11.jpg)
![12](./asset/image/12.jpg)
![13](./asset/image/13.jpg)
![14](./asset/image/14.jpg)