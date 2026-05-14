# Cron Jobs and Scripts on Ubuntu Server

## Introduction

A **Cron Job** is a scheduled task in Linux and Unix systems that runs automatically at a specified time or interval. Cron jobs are commonly used for:

- System maintenance
- Automated backups
- Log cleanup
- Running scripts
- Monitoring services
- Sending notifications
- Restarting services automatically

The service responsible for executing cron jobs is called **cron**.

---

# Understanding Cron

## What Is Cron?

Cron is a background service (daemon) that continuously checks scheduled tasks and executes them when their scheduled time arrives.

The configuration file for scheduled tasks is called a **crontab** (cron table).

---

# Checking Cron Service Status

## Verify Cron Service

Check whether the cron service is running:

```bash
sudo systemctl status cron
```

Example output:

```bash
● cron.service - Regular background program processing daemon
   Active: active (running)
```

---

## Start Cron Service

```bash
sudo systemctl start cron
```

---

## Enable Cron at Boot

```bash
sudo systemctl enable cron
```

---

# Crontab Basics

## Open Crontab Editor

Edit the current user's cron jobs:

```bash
crontab -e
```

When running for the first time, Ubuntu may ask you to choose an editor:

- nano
- vim
- etc.

Nano is recommended for beginners.

---

## View Existing Cron Jobs

```bash
crontab -l
```

---

## Remove All Cron Jobs

```bash
crontab -r
```

---

# Cron Job Syntax

A cron job has **five time fields** followed by the command.

```bash
* * * * * command_to_execute
- - - - -
| | | | |
| | | | +---- Day of Week (0 - 7)
| | | +------ Month (1 - 12)
| | +-------- Day of Month (1 - 31)
| +---------- Hour (0 - 23)
+------------ Minute (0 - 59)
```

---

# Time Field Explanation

| Field | Values | Description |
|---|---|---|
| Minute | 0-59 | Minute value |
| Hour | 0-23 | Hour value |
| Day of Month | 1-31 | Day number |
| Month | 1-12 | Month number |
| Day of Week | 0-7 | 0 and 7 = Sunday |

---

# Special Characters in Cron

| Character | Meaning |
|---|---|
| `*` | Every value |
| `,` | Multiple values |
| `-` | Range |
| `/` | Step values |

---

# Cron Schedule Examples

## Run Every Minute

```bash
* * * * * /home/user/script.sh
```

---

## Run Every 5 Minutes

```bash
*/5 * * * * /home/user/script.sh
```

---

## Run Every Hour

```bash
0 * * * * /home/user/script.sh
```

---

## Run Daily at Midnight

```bash
0 0 * * * /home/user/script.sh
```

---

## Run Daily at 6:30 AM

```bash
30 6 * * * /home/user/script.sh
```

---

## Run Every Sunday

```bash
0 0 * * 0 /home/user/script.sh
```

---

## Run on Specific Month and Day

```bash
0 0 1 1 * /home/user/newyear.sh
```

Runs every January 1st at midnight.

---

# Creating Bash Scripts for Cron Jobs

## Step 1: Create Script File

```bash
nano backup.sh
```

---

## Step 2: Add Script Content

Example:

```bash
#!/bin/bash

echo "Backup started at $(date)"
```

---

## Step 3: Make Script Executable

```bash
chmod +x backup.sh
```

---

## Step 4: Run Script Manually

```bash
./backup.sh
```

---

# Example Cron Job with Bash Script

Open crontab:

```bash
crontab -e
```

Add:

```bash
*/10 * * * * /home/user/backup.sh
```

This runs the script every 10 minutes.

---

# Using Full Paths in Cron Jobs

Cron uses a minimal environment.

Always use full paths for commands.

## Incorrect

```bash
backup.sh
```

---

## Correct

```bash
/var/scripts/backup.sh
```

---

# Finding Command Paths

Use:

```bash
which python3
which bash
which rsync
```

Example:

```bash
/usr/bin/python3
```

---

# Redirecting Output and Errors

Cron jobs can generate output.

## Save Output to File

```bash
*/5 * * * * /home/user/script.sh > /home/user/output.log
```

---

## Save Errors

```bash
*/5 * * * * /home/user/script.sh 2> /home/user/error.log
```

---

## Save Both Output and Errors

```bash
*/5 * * * * /home/user/script.sh >> /home/user/cron.log 2>&1
```

---

# Environment Variables in Cron

Cron does not load the normal shell environment.

You may need to define variables manually.

Example:

```bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

---

# Running Python Scripts with Cron

## Example Python Script

```python
print("Hello from Python")
```

Save as:

```bash
hello.py
```

---

## Make Script Executable

```bash
chmod +x hello.py
```

---

## Add Shebang

```python
#!/usr/bin/python3
```

---

## Cron Entry

```bash
*/5 * * * * /usr/bin/python3 /home/user/hello.py
```

---

# Running Backup Jobs

## Example Backup Script

```bash
#!/bin/bash

tar -czf /backup/home_backup.tar.gz /home/user
```

---

## Schedule Daily Backup

```bash
0 2 * * * /home/user/backup.sh
```

Runs every day at 2:00 AM.

---

# Automated Log Cleanup

## Cleanup Script

```bash
#!/bin/bash

find /var/log -name "*.log" -mtime +7 -delete
```

---

## Schedule Weekly Cleanup

```bash
0 0 * * 0 /home/user/cleanup.sh
```

---

# Restarting Services Automatically

## Restart Apache Every Day

```bash
0 3 * * * sudo systemctl restart apache2
```

---

# Cron Job Shortcuts

| Shortcut | Meaning |
|---|---|
| `@reboot` | Run at startup |
| `@hourly` | Every hour |
| `@daily` | Once per day |
| `@weekly` | Once per week |
| `@monthly` | Once per month |
| `@yearly` | Once per year |

---

# Examples Using Shortcuts

## Run Script at Boot

```bash
@reboot /home/user/startup.sh
```

---

## Run Daily

```bash
@daily /home/user/daily.sh
```

---

# System-Wide Cron Jobs

## System Crontab File

```bash
/etc/crontab
```

---

## Open System Crontab

```bash
sudo nano /etc/crontab
```

---

## Format of System Crontab

```bash
* * * * * user command
```

Example:

```bash
0 1 * * * root /root/backup.sh
```

---

# Cron Directories

| Directory | Purpose |
|---|---|
| `/etc/cron.hourly/` | Hourly jobs |
| `/etc/cron.daily/` | Daily jobs |
| `/etc/cron.weekly/` | Weekly jobs |
| `/etc/cron.monthly/` | Monthly jobs |

---

# Example Using cron.daily

Create script:

```bash
sudo nano /etc/cron.daily/cleanup
```

Make executable:

```bash
sudo chmod +x /etc/cron.daily/cleanup
```

---

# Viewing Cron Logs

## Ubuntu Syslog

```bash
grep CRON /var/log/syslog
```

---

## Live Monitoring

```bash
sudo tail -f /var/log/syslog
```

---

# Troubleshooting Cron Jobs

## Common Problems

### 1. Script Not Executable

Fix:

```bash
chmod +x script.sh
```

---

### 2. Incorrect Paths

Use full paths for:
- scripts
- commands
- files

---

### 3. Missing Permissions

Run with appropriate user privileges.

---

### 4. Environment Variable Issues

Define `PATH` manually.

---

### 5. Wrong Line Endings

Windows line endings can break scripts.

Fix:

```bash
dos2unix script.sh
```

---

# Best Practices

## Use Absolute Paths

Always use full file paths.

---

## Log Output

Keep logs for debugging.

---

## Test Scripts Manually

Before scheduling:

```bash
./script.sh
```

---

## Use Minimal Permissions

Avoid running cron jobs as root unless necessary.

---

## Comment Your Crontab

Example:

```bash
# Daily backup at 2 AM
0 2 * * * /home/user/backup.sh
```

---

# Real-World Examples

## Automatic Database Backup

```bash
0 1 * * * mysqldump -u root -pPASSWORD database > /backup/db.sql
```

---

## Disk Usage Monitoring

```bash
*/30 * * * * df -h > /home/user/disk_usage.log
```

---

## Website Availability Check

```bash
*/5 * * * * curl -I https://example.com
```

---

# Security Considerations

- Protect sensitive scripts
- Avoid storing passwords in plain text
- Restrict script permissions
- Monitor logs regularly
- Use secure backup locations

---

# Summary

Cron jobs are essential for Linux server automation. They allow administrators to:

- Automate repetitive tasks
- Schedule backups
- Run scripts automatically
- Monitor systems
- Clean logs
- Restart services

Understanding cron syntax and scripting helps improve server management and productivity on Ubuntu servers.