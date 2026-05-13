# Bash Scripting on Ubuntu Server

## Introduction

Bash scripting is the process of writing a series of commands in a text file that can be executed automatically by the Bash shell. Bash scripts help system administrators and developers automate repetitive tasks such as backups, system updates, user management, monitoring, and deployment.

Ubuntu Server uses **Bash (Bourne Again Shell)** as the default command-line shell.

---

# Objectives

By the end of this documentation, you will learn:

- What Bash scripting is
- How to create and run Bash scripts
- Bash script syntax and structure
- Variables and user input
- Conditional statements
- Loops
- Functions
- File permissions
- Practical automation examples

---

# Environment

| Component | Details |
|---|---|
| Operating System | Ubuntu Server 26.04 |
| Shell | Bash |
| Editor | Nano / Vim |
| Terminal | Ubuntu Server CLI |

---

# What is Bash?

Bash is a command-line interpreter used in Linux systems.

It allows users to:

- Execute Linux commands
- Automate tasks
- Manage files and users
- Create shell scripts

Check the current shell:

```bash
echo $SHELL
```

Example output:

```bash
/bin/bash
```

---

# What is a Bash Script?

A Bash script is a file containing Linux commands executed sequentially.

Example:

```bash
#!/bin/bash
echo "Hello World"
```

---

# Script File Extension

Bash scripts commonly use:

```text
.sh
```

Example:

```text
backup.sh
update.sh
```

---

# Step 1 — Create a Bash Script

Create a new script file:

```bash
nano hello.sh
```

Add the following content:

```bash
#!/bin/bash

echo "Hello, Ubuntu Server!"
```

Save the file:

```text
CTRL + O → Enter → CTRL + X
```

---

# Step 2 — Make Script Executable

By default, scripts are not executable.

Use:

```bash
chmod +x hello.sh
```

Verify permissions:

```bash
ls -l hello.sh
```

Example output:

```bash
-rwxr-xr-x 1 user user 45 May 14 10:00 hello.sh
```

---

# Step 3 — Run the Script

Execute the script:

```bash
./hello.sh
```

Output:

```bash
Hello, Ubuntu Server!
```

---

# Understanding the Shebang

The first line:

```bash
#!/bin/bash
```

is called the **Shebang**.

It tells Linux to execute the script using the Bash interpreter.

---

# Comments in Bash

Comments help describe code.

Single-line comment:

```bash
# This is a comment
```

Example:

```bash
#!/bin/bash

# Display welcome message
echo "Welcome"
```

---

# Variables in Bash

Variables store data.

Example:

```bash
#!/bin/bash

name="Thant"
echo "Hello $name"
```

Output:

```bash
Hello Thant
```

---

# User Input

Use `read` to accept user input.

Example:

```bash
#!/bin/bash

echo "Enter your name:"
read username

echo "Welcome $username"
```

---

# Command-Line Arguments

Scripts can accept arguments.

Example:

```bash
#!/bin/bash

echo "First argument: $1"
echo "Second argument: $2"
```

Run:

```bash
./script.sh Ubuntu Server
```

Output:

```bash
First argument: Ubuntu
Second argument: Server
```

---

# Important Special Variables

| Variable | Description |
|---|---|
| `$0` | Script name |
| `$1-$9` | Arguments |
| `$#` | Number of arguments |
| `$?` | Exit status |
| `$$` | Process ID |

Example:

```bash
echo "Script Name: $0"
echo "Argument Count: $#"
```

---

# Conditional Statements

## if Statement

Example:

```bash
#!/bin/bash

number=10

if [ $number -gt 5 ]
then
    echo "Number is greater than 5"
fi
```

---

# if-else Statement

Example:

```bash
#!/bin/bash

read -p "Enter password: " pass

if [ "$pass" = "admin123" ]
then
    echo "Access Granted"
else
    echo "Access Denied"
fi
```

---

# Comparison Operators

| Operator | Meaning |
|---|---|
| `-eq` | Equal |
| `-ne` | Not Equal |
| `-gt` | Greater Than |
| `-lt` | Less Than |
| `-ge` | Greater or Equal |
| `-le` | Less or Equal |

---

# Loops in Bash

## for Loop

Example:

```bash
#!/bin/bash

for i in 1 2 3 4 5
do
    echo "Number: $i"
done
```

---

# while Loop

Example:

```bash
#!/bin/bash

count=1

while [ $count -le 5 ]
do
    echo "Count: $count"
    ((count++))
done
```

---

# Functions in Bash

Functions organize reusable code.

Example:

```bash
#!/bin/bash

greet() {
    echo "Welcome to Ubuntu Server"
}

greet
```

---

# File and Directory Operations

## Create Directory

```bash
mkdir backup
```

## Create File

```bash
touch test.txt
```

## Copy File

```bash
cp file1.txt backup/
```

## Remove File

```bash
rm file1.txt
```

---

# Using Date and Time

Example:

```bash
#!/bin/bash

echo "Current Date:"
date
```

---

# System Information Script

Example:

```bash
#!/bin/bash

echo "Hostname: $(hostname)"
echo "Current User: $(whoami)"
echo "Kernel Version:"
uname -r
```

---

# Backup Script Example

Create backup script:

```bash
nano backup.sh
```

Script:

```bash
#!/bin/bash

backup_dir="/backup"
source_dir="/home"

mkdir -p $backup_dir

tar -czvf $backup_dir/home_backup.tar.gz $source_dir

echo "Backup Completed"
```

Make executable:

```bash
chmod +x backup.sh
```

Run:

```bash
./backup.sh
```

---

# Automatic System Update Script

Example:

```bash
#!/bin/bash

sudo apt update
sudo apt upgrade -y

echo "System Updated Successfully"
```

---

# Exit Status

Linux commands return exit codes.

Check status:

```bash
echo $?
```

| Exit Code | Meaning |
|---|---|
| `0` | Success |
| Non-zero | Error |

---

# Debugging Bash Scripts

Run script in debug mode:

```bash
bash -x script.sh
```

Example:

```bash
bash -x hello.sh
```

---

# Scheduling Scripts with Cron

Open cron table:

```bash
crontab -e
```

Example — run backup daily at midnight:

```bash
0 0 * * * /home/user/backup.sh
```

---

# Best Practices

- Use meaningful script names
- Add comments
- Test scripts before production use
- Use absolute paths
- Keep backups of important scripts
- Use proper permissions

---

# Common Bash Commands

| Command | Description |
|---|---|
| `echo` | Display text |
| `read` | Read user input |
| `chmod` | Change permissions |
| `date` | Display date/time |
| `tar` | Archive files |
| `grep` | Search text |
| `awk` | Text processing |
| `sed` | Stream editor |

---

# Verification

Check Bash version:

```bash
bash --version
```

Check script permissions:

```bash
ls -l script.sh
```

Run script:

```bash
./script.sh
```

---

# Troubleshooting

## Permission Denied

Fix:

```bash
chmod +x script.sh
```

---

## Bad Interpreter Error

Check shebang:

```bash
#!/bin/bash
```

---

## Command Not Found

Install missing package:

```bash
sudo apt install package-name
```

---

# Conclusion

Bash scripting is an essential skill for Ubuntu Server administration. It allows administrators to automate repetitive tasks, improve efficiency, and manage systems more effectively.

With Bash scripts, you can:

- Automate server maintenance
- Manage backups
- Monitor systems
- Deploy applications
- Simplify administration tasks

Learning Bash scripting is a fundamental step toward becoming a Linux system administrator or DevOps engineer.