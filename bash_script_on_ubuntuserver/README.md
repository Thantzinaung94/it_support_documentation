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