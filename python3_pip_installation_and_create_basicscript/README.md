# Python 3 Installation and Basic Usage on Ubuntu Server 26.04

## Objective

This documentation explains how to:

- Install Python 3 on Ubuntu Server 26.04
- Install Python package management tools (`pip`)
- Write a basic Python script
- Run the Python script from the terminal

---

# 1. Update Package Repository

Before installing software, update the package repository.

```bash
sudo apt update
```

---

# 2. Install Python 3

Install Python on Ubuntu Server using the following command:

```bash
sudo apt install python3 -y
```

> Note:
> The command `sudo apt install python` may not work on some Ubuntu versions because Python 2 packages are deprecated.  
> Ubuntu Server 26.04 uses `python3`.

---

# 3. Verify Python Installation

Check the installed Python version:

```bash
python3 --version
```

### Example Output

```bash
Python 3.14.0
```

---

# 4. Install Python Pip (Python Package Manager)

Install `pip` for managing Python libraries and packages.

```bash
sudo apt install python3-pip -y
```

---

# 5. Verify Pip Installation

Check the installed pip version:

```bash
pip3 --version
```

### Example Output

```bash
pip 25.0 from /usr/lib/python3/dist-packages/pip (python 3.14)
```

---

# 6. Install Python Libraries

Use `pip3` to install Python libraries.

## Example: Install Requests Library

```bash
pip3 install requests
```

---

# 7. Create a Python Script

Create a new Python file using the `nano` text editor.

```bash
nano hello.py
```

Add the following Python code:

```python
print("Hello, Ubuntu Server 26.04")
print("Python is working successfully!")
```

### Save the File

- Press `CTRL + O` → Enter
- Press `CTRL + X`

---

# 8. Run the Python Script

Execute the script using Python 3.

```bash
python3 hello.py
```

### Example Output

```bash
Hello, Ubuntu Server 26.04
Python is working successfully!
```

---

# 9. Display Python Script Files

List Python files in the current directory:

```bash
ls *.py
```

---

# 10. Remove a Python Library

Example: Remove the `requests` library.

```bash
pip3 uninstall requests
```

---

# 11. Useful Python Commands

| Command | Description |
|---|---|
| `python3 --version` | Check Python version |
| `pip3 --version` | Check pip version |
| `python3 filename.py` | Run Python script |
| `pip3 install package-name` | Install Python package |
| `pip3 uninstall package-name` | Remove Python package |
| `pip3 list` | Show installed packages |

---

# 12. Verification

Verify that:

- Python 3 is installed successfully
- Pip is working correctly
- Python scripts can execute without errors
- Python libraries can be installed using `pip3`

---

# Conclusion

In this lab, Python 3 and `pip` were successfully installed on Ubuntu Server 26.04. A basic Python script was created and executed successfully, confirming that the Python environment is working properly.