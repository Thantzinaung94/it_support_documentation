# Bash Scripting Documentation

## Introduction

Bash scripting is a powerful way to automate tasks in Linux systems such as Ubuntu Server. A Bash script is a text file containing a series of commands that are executed by the Bash shell.

Bash scripts are commonly used for:

- System administration
- Automation tasks
- File management
- Backup operations
- Monitoring services
- User management

---

# Bash Scripting Cheat Sheet

## ✅ Basic Structure

Every Bash script usually starts with a *shebang* line that tells the system which interpreter to use.

```bash
#!/bin/bash

# This is a comment
echo "Hello, world!"
```

### Explanation

- `#!/bin/bash` → Defines Bash as the script interpreter
- `#` → Used for comments
- `echo` → Prints text to the terminal

---

# 📁 Running a Script

Before running a script, make it executable using the `chmod` command.

```bash
chmod +x script.sh     # Make it executable
./script.sh            # Run the script
```

### Explanation

- `chmod +x` → Adds execute permission
- `./script.sh` → Executes the script from the current directory

---

# 📦 Variables

Variables store data that can be reused later in the script.

```bash
name="Dan"
echo "Hello, $name"
```

### Explanation

- `name="Dan"` → Creates a variable
- `$name` → Accesses the variable value

### Output

```bash
Hello, Dan
```

---

# 💬 User Input

Use the `read` command to get input from the user.

```bash
read -p "Enter your name: " username
echo "Welcome, $username!"
```

### Explanation

- `read` → Accepts user input
- `-p` → Displays a prompt message

---

# 📄 Conditionals

Conditionals allow scripts to make decisions.

```bash
if [ "$name" == "admin" ]; then
  echo "Access granted."
else
  echo "Access denied."
fi
```

### Explanation

- `if` → Starts a condition
- `then` → Runs commands if true
- `else` → Runs commands if false
- `fi` → Ends the condition block

---

# 🔁 Loops

Loops repeat commands multiple times.

## For Loop

```bash
for i in {1..5}; do
  echo "Number $i"
done
```

### Output

```bash
Number 1
Number 2
Number 3
Number 4
Number 5
```

---

## While Loop

```bash
count=1

while [ $count -le 3 ]; do
  echo "Count: $count"
  ((count++))
done
```

### Explanation

- `-le` → Less than or equal to
- `((count++))` → Increments the value

---

# ⚙️ Functions

Functions help organize reusable code blocks.

```bash
greet() {
  echo "Hello, $1!"
}

greet "Dan"
```

### Explanation

- `greet()` → Function name
- `$1` → First argument passed to the function

---

# 🧮 Arithmetic Operations

Bash supports basic arithmetic calculations.

```bash
a=5
b=3

sum=$((a + b))

echo "Sum is $sum"
```

### Output

```bash
Sum is 8
```

---

# 📦 Arrays

Arrays store multiple values in a single variable.

```bash
fruits=("apple" "banana" "cherry")

echo "${fruits[1]}"     # banana
echo "${fruits[@]}"     # all elements
```

### Explanation

- `${fruits[1]}` → Access second element
- `${fruits[@]}` → Display all elements

---

# 📂 File and Directory Checks

Check whether files or directories exist.

## File Check

```bash
if [ -f "file.txt" ]; then
  echo "File exists."
fi
```

## Directory Check

```bash
if [ -d "/etc" ]; then
  echo "Directory exists."
fi
```

### Common Test Operators

| Operator | Meaning |
|---|---|
| `-f` | File exists |
| `-d` | Directory exists |
| `-r` | Readable |
| `-w` | Writable |
| `-x` | Executable |

---

# 🗃️ Command Substitution

Store command output inside a variable.

```bash
date_today=$(date)

echo "Today is $date_today"
```

### Explanation

- `$(command)` → Executes command and stores output

---

# 🐛 Error Handling

Use logical operators to handle errors.

```bash
command || echo "Command failed"
```

### Explanation

- `||` → Runs the second command if the first fails

---

# 🔁 Case Statement

Case statements are useful for menu systems and choices.

```bash
read -p "Enter choice: " choice

case $choice in
  y|Y) echo "You chose yes";;
  n|N) echo "You chose no";;
  *)   echo "Invalid choice";;
esac
```

### Explanation

- `case` → Starts case statement
- `;;` → Ends each option
- `*` → Default case

---

# 🕓 Cron Jobs and Scripts

Cron jobs automate script execution at scheduled times.

## Open Crontab

```bash
crontab -e
```

## Run Script Every Day at 6 AM

```bash
0 6 * * * /home/user/scripts/myscript.sh
```

### Cron Format

```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week
│ │ │ └──── Month
│ │ └────── Day
│ └──────── Hour
└────────── Minute
```

---

# 📜 Logging Output

Save script output into a log file.

```bash
echo "Starting task..." >> /var/log/myscript.log
```

### Explanation

- `>>` → Appends output to a file

---

# 🔒 Script Permissions

Manage permissions for security.

```bash
chmod +x myscript.sh     # Make executable
chmod 700 myscript.sh    # Only owner can run
```

### Permission Meaning

| Permission | Description |
|---|---|
| 700 | Owner has full access |
| 755 | Owner full, others read/execute |
| 644 | Owner read/write, others read |

---

# 📌 Best Practices

## Always Start with Shebang

```bash
#!/bin/bash
```

---

## Use Comments

```bash
# Backup important files
```

Comments improve readability and maintenance.

---

## Quote Variables

```bash
echo "$username"
```

This prevents issues with spaces and special characters.

---

## Test Scripts Safely

- Test scripts in a non-production environment
- Avoid running dangerous commands as root
- Verify scripts before automation

---

# Example Full Bash Script

```bash
#!/bin/bash

# Simple user greeting script

read -p "Enter your name: " username

if [ "$username" == "admin" ]; then
  echo "Welcome Administrator!"
else
  echo "Welcome, $username!"
fi

echo "Today's date is $(date)"
```

---

# Conclusion

Bash scripting is an essential skill for Linux system administrators and DevOps engineers. By learning variables, loops, functions, conditionals, and automation tools like Cron, users can automate repetitive tasks and manage servers more efficiently.

With regular practice, Bash scripting becomes a powerful tool for managing Ubuntu Server environments.