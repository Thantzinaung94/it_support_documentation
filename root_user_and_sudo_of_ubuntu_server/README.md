# Ubuntu Server 26 – Root User and `sudo` Command Documentation

## 1. Objective

This document explains the concept of the **root user** and the usage of the **`sudo` command** in Ubuntu Server 26. It includes command examples, permission management, and security best practices for Linux system administration.

---

# 2. Introduction

Ubuntu Server uses a security model where administrative tasks are normally performed using the `sudo` command instead of logging in directly as the root user.

## Root User

The **root user** is the highest privileged account in Linux systems.

It has unrestricted access to all files, commands, and system settings.

## `sudo`

The **`sudo`** command allows authorized users to execute commands with root privileges temporarily.

---

# 3. Root User in Ubuntu Server 26

## 3.1 What is Root User?

The root account:

- Has full control over the system
- Can install/remove software
- Can modify system files
- Can manage users and permissions
- Can start/stop services

Default root username:

```bash
root
```

---

## 3.2 Check Current Logged-in User

```bash
whoami
```

Example output:

```bash
ubuntu
```

---

## 3.3 Check Current User ID

```bash
id
```

Example output:

```bash
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),27(sudo)
```

---

## 3.4 Switch to Root User

### Method 1 — Using sudo

```bash
sudo -i
```

OR

```bash
sudo su
```

Example:

```bash
ubuntu@server:~$ sudo -i
root@server:~#
```

The `#` symbol indicates root access.

---

## 3.5 Exit Root User

```bash
exit
```

---

# 4. Set Root Password

By default, Ubuntu disables direct root login.

To set a root password:

```bash
sudo passwd root
```

Example:

```bash
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

---

# 5. Lock Root Account

To disable root login again:

```bash
sudo passwd -l root
```

---

# 6. Unlock Root Account

```bash
sudo passwd -u root
```

---

# 7. Understanding `sudo`

## 7.1 What is `sudo`?

`sudo` means:

```text
SuperUser DO
```

It allows normal users to execute administrative commands safely.

---

## 7.2 Basic Syntax

```bash
sudo <command>
```

Example:

```bash
sudo apt update
```

---

# 8. Common sudo Commands

## 8.1 Update Package List

```bash
sudo apt update
```

---

## 8.2 Install Software

```bash
sudo apt install nginx
```

---

## 8.3 Restart Service

```bash
sudo systemctl restart ssh
```

---

## 8.4 Edit System File

```bash
sudo nano /etc/hosts
```

---

## 8.5 View Root Directory

```bash
sudo ls /root
```

---

# 9. Add User to sudo Group

Users in the `sudo` group can use administrative commands.

## Command

```bash
sudo usermod -aG sudo username
```

Example:

```bash
sudo usermod -aG sudo hantun
```

---

# 10. Verify sudo Access

## Check User Groups

```bash
groups username
```

Example:

```bash
groups hantun
```

Output:

```bash
hantun : hantun sudo
```

---

# 11. Remove User from sudo Group

```bash
sudo deluser username sudo
```

Example:

```bash
sudo deluser hantun sudo
```

---

# 12. Check sudo Privileges

```bash
sudo -l
```

This displays commands the user is allowed to execute.

---

# 13. sudo Configuration File

The sudo configuration file:

```bash
/etc/sudoers
```

Do NOT edit directly using normal editors.

Use:

```bash
sudo visudo
```

This prevents syntax errors.

---

# 14. Example sudoers Entry

Example permission:

```bash
hantun ALL=(ALL:ALL) ALL
```

Meaning:

| Field | Description |
|---|---|
| hantun | Username |
| ALL | Any host |
| (ALL:ALL) | Any user/group |
| ALL | Any command |

---

# 15. Security Best Practices

## Recommended Practices

### Use sudo Instead of Root Login

- Safer than permanent root access
- Commands are logged

### Use Strong Passwords

- Protect administrator accounts

### Avoid Direct SSH Root Login

Recommended setting in:

```bash
/etc/ssh/sshd_config
```

Set:

```bash
PermitRootLogin no
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

### Grant Minimum Required Permissions

- Only trusted users should have sudo access

---

# 16. Troubleshooting

## 16.1 “user is not in the sudoers file”

Error:

```bash
username is not in the sudoers file
```

Fix using root account:

```bash
usermod -aG sudo username
```

---

## 16.2 sudo Command Not Found

Install sudo:

```bash
apt install sudo
```

---

## 16.3 Permission Denied

Ensure:

- User belongs to `sudo` group
- Correct password is entered

Check groups:

```bash
groups
```

---

# 17. Verification Commands

| Task | Command |
|---|---|
| Check current user | `whoami` |
| Check user ID | `id` |
| Switch to root | `sudo -i` |
| Exit root | `exit` |
| Set root password | `sudo passwd root` |
| Lock root account | `sudo passwd -l root` |
| Unlock root account | `sudo passwd -u root` |
| Add sudo access | `sudo usermod -aG sudo username` |
| Remove sudo access | `sudo deluser username sudo` |
| Check sudo permissions | `sudo -l` |

---

# 18. Conclusion

The root user and `sudo` command are essential components of Ubuntu Server 26 administration. Using `sudo` provides a secure and controlled method for performing administrative tasks while reducing security risks associated with direct root access.

System administrators should always follow security best practices by limiting root usage, granting minimal permissions, and using sudo for daily administrative operations.