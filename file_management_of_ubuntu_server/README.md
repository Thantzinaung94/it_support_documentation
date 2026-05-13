# Additional File Viewing Commands in Ubuntu Server 26.04

These commands are commonly used for reading, monitoring, and navigating file contents in Ubuntu Server.

---

# 25. Using `cat` Command

## Purpose
Displays the entire content of a file.

## Syntax
```bash
cat filename
```

## Example
```bash
cat file1.txt
```

## Create File Using cat
```bash
cat > notes.txt
```

Type text and press:

```bash
CTRL + D
```

to save the file.

## Display Line Numbers
```bash
cat -n file1.txt
```

---

# 26. Using `less` Command

## Purpose
Views large files page by page.

## Syntax
```bash
less filename
```

## Example
```bash
less /var/log/syslog
```

## Navigation Keys

| Key | Function |
|---|---|
| Up/Down Arrow | Move line |
| Space | Next page |
| b | Previous page |
| /word | Search word |
| q | Quit |

## Advantages
- Better for large files
- Faster than `cat`
- Search support

---

# 27. Using `more` Command

## Purpose
Displays file content one page at a time.

## Syntax
```bash
more filename
```

## Example
```bash
more file1.txt
```

## Navigation

| Key | Function |
|---|---|
| Space | Next page |
| Enter | Next line |
| q | Quit |

---

# 28. Using `head` Command

## Purpose
Displays the beginning lines of a file.

## Default
Shows first 10 lines.

## Syntax
```bash
head filename
```

## Example
```bash
head file1.txt
```

## Show Specific Number of Lines
```bash
head -5 file1.txt
```

---

# 29. Using `tail` Command

## Purpose
Displays the last lines of a file.

## Default
Shows last 10 lines.

## Syntax
```bash
tail filename
```

## Example
```bash
tail /var/log/syslog
```

## Show Specific Number of Lines
```bash
tail -20 file1.txt
```

---

# 30. Real-Time Monitoring with `tail -f`

## Purpose
Monitors file updates in real time.

## Syntax
```bash
tail -f filename
```

## Example
```bash
tail -f /var/log/auth.log
```

## Usage
Useful for:
- System logs
- Server monitoring
- Debugging services

## Stop Monitoring
Press:

```bash
CTRL + C
```

---

# 31. Using `tac` Command

## Purpose
Displays file contents in reverse order.

## Syntax
```bash
tac filename
```

## Example
```bash
tac file1.txt
```

---

# 32. Using `nl` Command

## Purpose
Displays file content with line numbers.

## Syntax
```bash
nl filename
```

## Example
```bash
nl file1.txt
```

---

# 33. Using `wc` Command

## Purpose
Counts lines, words, and characters in a file.

## Syntax
```bash
wc filename
```

## Example
```bash
wc file1.txt
```

## Output Example
```bash
20 100 800 file1.txt
```

Meaning:
- 20 lines
- 100 words
- 800 characters

## Count Only Lines
```bash
wc -l file1.txt
```

---

# 34. Using `grep` Command

## Purpose
Searches text patterns inside files.

## Syntax
```bash
grep "word" filename
```

## Example
```bash
grep "error" /var/log/syslog
```

## Ignore Upper/Lower Case
```bash
grep -i "error" file1.txt
```

## Show Line Numbers
```bash
grep -n "error" file1.txt
```

---

# 35. Using `sort` Command

## Purpose
Sorts file content alphabetically.

## Syntax
```bash
sort filename
```

## Example
```bash
sort names.txt
```

## Reverse Sort
```bash
sort -r names.txt
```

---

# 36. Using `uniq` Command

## Purpose
Removes duplicate lines.

## Syntax
```bash
uniq filename
```

## Example
```bash
uniq names.txt
```

## Count Duplicates
```bash
uniq -c names.txt
```

---

# 37. Using `cut` Command

## Purpose
Extracts specific columns from files.

## Syntax
```bash
cut -d "delimiter" -f field filename
```

## Example
```bash
cut -d ":" -f 1 /etc/passwd
```

Displays usernames from `/etc/passwd`.

---

# 38. Using `paste` Command

## Purpose
Merges lines from multiple files.

## Example
```bash
paste file1.txt file2.txt
```

---

# 39. Using `tee` Command

## Purpose
Displays output and saves it to a file.

## Example
```bash
ls | tee filelist.txt
```

## Append Output
```bash
ls | tee -a filelist.txt
```

---

# 40. Using `stat` Command

## Purpose
Displays detailed file information.

## Example
```bash
stat file1.txt
```

## Information Includes
- File size
- Permissions
- Owner
- Last access time
- Modification time

---

# Verification Commands

## Verify File Content
```bash
cat file1.txt
```

## Verify Last Log Updates
```bash
tail -f /var/log/syslog
```

## Verify Search Results
```bash
grep "error" /var/log/syslog
```

---

# Summary Table

| Command | Description |
|---|---|
| `cat` | Display file content |
| `less` | View large files |
| `more` | Page-by-page viewer |
| `head` | Show first lines |
| `tail` | Show last lines |
| `tail -f` | Real-time monitoring |
| `tac` | Reverse display |
| `nl` | Show line numbers |
| `wc` | Count lines/words |
| `grep` | Search text |
| `sort` | Sort content |
| `uniq` | Remove duplicates |
| `cut` | Extract columns |
| `paste` | Merge files |
| `tee` | Save output |
| `stat` | File details |

---

# Conclusion

These file viewing and text-processing commands are essential for Linux system administration in Ubuntu Server 26.04. They help administrators efficiently inspect logs, analyze files, search data, and monitor system activity from the command line.

![Linux_File_Permissions_Cheat_Sheet](./asset/Linux_File_Permissions_Cheat_Sheet.pdf)
![ubuntu_file_management](./asset/ubuntu_file_management.pdf)