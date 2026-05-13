# FIGlet, Lolcat, and Neofetch Configuration on Ubuntu

## Objective

This document explains how to install and configure the following Linux terminal customization tools on Ubuntu:

- `figlet`
- `lolcat`
- `neofetch`

The configuration displays a colorful welcome banner using `figlet` and `lolcat`, and automatically shows system information using `neofetch` whenever a new terminal session starts.

---

# 1. Environment

| Component | Details |
|---|---|
| Operating System | Ubuntu Linux |
| Shell | Bash |
| Configuration File | `~/.bashrc` |

---

# 2. Install Required Packages

Update the package list before installation.

```bash
sudo apt update
```

Install `figlet` and `neofetch`.

```bash
sudo apt install figlet neofetch -y
```

Install `lolcat`.

```bash
sudo apt install lolcat -y
```

---

# 3. FIGlet Command

## Purpose

`figlet` is used to create large ASCII text banners in the terminal.

## Syntax

```bash
figlet [options] "text"
```

## Example

```bash
figlet "Hello"
```

### Output Example

```text
 _   _      _ _
| | | | ___| | | ___
| |_| |/ _ \ | |/ _ \
|  _  |  __/ | | (_) |
|_| |_|\___|_|_|\___/
```

---

# 4. Lolcat Command

## Purpose

`lolcat` adds rainbow colors and animation effects to terminal output.

## Syntax

```bash
command | lolcat
```

## Example

```bash
figlet "Welcome" | lolcat
```

---

# 5. Customized Welcome Banner

## Configured Command

The following command was used:

```bash
figlet -f slant "Hello, Mr.Thantzinaung, Mingalarpar" | lolcat -a -d 2
```

## Command Explanation

| Option | Description |
|---|---|
| `-f slant` | Uses the `slant` font style in figlet |
| `lolcat` | Applies rainbow color output |
| `-a` | Enables animation |
| `-d 2` | Sets animation delay speed |

---

# 6. Neofetch Command

## Purpose

`neofetch` displays system information such as:

- OS version
- Kernel version
- CPU
- Memory usage
- Shell
- Terminal
- Uptime

## Syntax

```bash
neofetch
```

## Example Output

```text
OS: Ubuntu 24.04
Kernel: 6.x.x
Shell: bash
CPU: Intel/AMD Processor
Memory: 4GB / 8GB
```

---

# 7. Configure Automatic Startup in ~/.bashrc

## Open the Bash Configuration File

```bash
nano ~/.bashrc
```

## Add the Following Lines at the Bottom

```bash
figlet -f slant "Hello, Mr.Thantzinaung, Mingalarpar" | lolcat -a -d 2

neofetch
```

---

# 8. Apply the Changes

Reload the bash configuration.

```bash
source ~/.bashrc
```

---

# 9. Verification

## Open a New Terminal Session

When a new terminal opens:

1. A colorful welcome banner appears.
2. System information from `neofetch` is displayed automatically.

---

# 10. Troubleshooting

## Issue: Command Not Found

### Fix

Install the missing package again.

```bash
sudo apt install figlet lolcat neofetch -y
```

---

## Issue: ~/.bashrc Changes Not Working

### Fix

Reload the configuration manually.

```bash
source ~/.bashrc
```

---

# 11. Conclusion

The terminal was customized successfully using:

- `figlet` for ASCII banner text
- `lolcat` for colorful animated output
- `neofetch` for displaying system information

These tools improve the terminal appearance and provide useful system details automatically during login or terminal startup.