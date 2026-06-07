# Linux Mint Essential Commands – Hands-On Lab

## Lab Information

| Item | Details |
|--------|---------|
| Operating System | Linux Mint 22.3 Cinnamon (64-bit) |
| Environment | Hyper-V Virtual Machine |
| RAM | 4 GB |
| Storage | 50 GB |
| Username | thantzinaung |
| Hostname | linux-mint |
| Difficulty | Beginner to Intermediate |
| Duration | 2-3 Hours |

---

# Objective

In this lab:

- Navigate the Linux filesystem
- Manage files and directories
- View and edit files
- Manage users and permissions
- Monitor system resources
- Install and update software
- Work with networking commands
- Use process management commands
- Access help documentation

---

# Lab Topology

```text
+--------------------------------+
|      Linux Mint 22.3 VM        |
|--------------------------------|
| Hostname : linux-mint          |
| User     : thantzinaung        |
| RAM      : 4 GB                |
| Disk     : 50 GB               |
+--------------------------------+
```

---

# Open Terminal

## Method 1

Press:

```text
Ctrl + Alt + T
```

## Method 2

```text
Menu → Terminal
```

Verify current user:

```bash
whoami
```

Expected Output:

```text
thantzinaung
```

---

# Basic Navigation Commands

## Check Current Directory

```bash
pwd
```

Example:

```text
/home/thantzinaung
```

## List Files and Folders

```bash
ls
```

Detailed View:

```bash
ls -l
```

Show Hidden Files:

```bash
ls -la
```

## Change Directory

Move to Documents:

```bash
cd Documents
```

Return Home:

```bash
cd
```

Move One Level Up:

```bash
cd ..
```

---

# Exercise 3: Creating Directories

Create a directory:

```bash
mkdir LinuxLab
```

Verify:

```bash
ls
```

Create multiple directories:

```bash
mkdir Lab1 Lab2 Lab3
```

---

# Exercise 4: Creating Files

Create an empty file:

```bash
touch file1.txt
```

Create multiple files:

```bash
touch file2.txt file3.txt
```

Verify:

```bash
ls
```

---

# Viewing File Contents

Create sample text:

```bash
echo "Welcome to Linux Mint Lab" > lab.txt
```

Display content:

```bash
cat lab.txt
```

View page by page:

```bash
less lab.txt
```

Display first lines:

```bash
head lab.txt
```

Display last lines:

```bash
tail lab.txt
```

---

# Copying Files

Create source file:

```bash
touch source.txt
```

Copy file:

```bash
cp source.txt backup.txt
```

Verify:

```bash
ls
```

---

# Moving and Renaming Files

Rename file:

```bash
mv backup.txt backup-old.txt
```

Move file to another folder:

```bash
mv backup-old.txt LinuxLab/
```

---

# Removing Files and Directories

Delete file:

```bash
rm file1.txt
```

Delete directory:

```bash
rmdir Lab1
```

Delete non-empty directory:

```bash
rm -r LinuxLab
```

---

# Searching Files

Find file:

```bash
find ~ -name lab.txt
```

Locate command:

```bash
locate lab.txt
```

Update database:

```bash
sudo updatedb
```

---

#rm File Permissions

Check permissions:

```bash
ls -l
```

Example:

```text
-rw-r--r--
```

Change permissions:

```bash
chmod 755 script.sh
```

Verify:

```bash
ls -l script.sh
```

---

# File Ownership

View ownership:

```bash
ls -l
```

Change ownership:

```bash
sudo chown thantzinaung file.txt
```

Change group:

```bash
sudo chgrp users file.txt
```

---

# User Management

View current user:

```bash
whoami
```

Display user ID:

```bash
id
```

Create new user:

```bash
sudo adduser student1
```

Switch user:

```bash
su - student1
```

Delete user:

```bash
sudo deluser student1
```

---

# Package Management (APT)

Update repository:

```bash
sudo apt update
```

Upgrade packages:

```bash
sudo apt upgrade -y
```

Install package:

```bash
sudo apt install tree -y
```

Verify:

```bash
tree
```

Remove package:

```bash
sudo apt remove tree -y
```

---

# Exercise 14: Disk Management Commands

Check disk usage:

```bash
df -h
```

Check directory size:

```bash
du -sh ~/Documents
```

View block devices:

```bash
lsblk
```

---

# Memory and CPU Monitoring

View memory usage:

```bash
free -h
```

Display CPU information:

```bash
lscpu
```

Monitor processes:

```bash
top
```

Modern alternative:

```bash
htop
```

Install htop:

```bash
sudo apt install htop -y
```

---

# Exercise 16: Process Management

View running processes:

```bash
ps aux
```

Find process:

```bash
ps aux | grep firefox
```

Terminate process:

```bash
kill PID
```

Force terminate:

```bash
kill -9 PID
```

---

# Exercise 17: Networking Commands

Display IP Address:

```bash
ip addr
```

Display routing table:

```bash
ip route
```

Test connectivity:

```bash
ping google.com
```

DNS lookup:

```bash
nslookup google.com
```

Check open ports:

```bash
ss -tulnp
```

---

# System Information

Display hostname:

```bash
hostname
```

Display kernel version:

```bash
uname -r
```

Display OS information:

```bash
cat /etc/os-release
```

Display uptime:

```bash
uptime
```

---

# Archive and Compression

Create archive:

```bash
tar -cvf backup.tar Documents
```

Extract archive:

```bash
tar -xvf backup.tar
```

Compress archive:

```bash
tar -czvf backup.tar.gz Documents
```

Extract compressed archive:

```bash
tar -xzvf backup.tar.gz
```

---

# Command Help

Get help:

```bash
man ls
```

Command help:

```bash
ls --help
```

Search manual pages:

```bash
man -k network
```

---

# Verification Checklist

| Task | Status |
|--------|---------|
| Navigate directories | □ |
| Create files | □ |
| Create folders | □ |
| Copy files | □ |
| Move files | □ |
| Delete files | □ |
| Search files | □ |
| Manage permissions | □ |
| Manage users | □ |
| Install packages | □ |
| Monitor system | □ |
| Test network | □ |
| Compress files | □ |

---

## Key Commands Learned

```text
pwd
ls
cd
mkdir
touch
cp
mv
rm
find
chmod
chown
apt
df
du
free
top
ps
kill
ip
ping
tar
man
```

---
![mint_linux_essential_commands](./asset/image/mint_linux_essential_commands.png)
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
![15](./asset/image/15.jpg)