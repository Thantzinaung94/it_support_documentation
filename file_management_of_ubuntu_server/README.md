# File Management of Ubuntu Server 26.04

## Objective
This document explains basic and advanced file management commands in Ubuntu Server 26.04. It includes creating, viewing, copying, moving, deleting, searching, compressing, and changing permissions of files and directories.

---

# Environment

| Item | Description |
|---|---|
| Operating System | Ubuntu Server 26.04 |
| Shell | Bash |
| User Type | Root / Sudo User |
| Terminal | Ubuntu Terminal / SSH |

---

# 1. Understanding Linux File System

Linux stores everything as files.

Common directories:

| Directory | Purpose |
|---|---|
| `/home` | User home directories |
| `/etc` | Configuration files |
| `/var` | Logs and variable data |
| `/tmp` | Temporary files |
| `/root` | Root user home |
| `/usr` | User programs and packages |

---

# 2. Check Current Directory

## Command
```bash
pwd
```

## Explanation
Displays the current working directory.

## Example Output
```bash
/home/student
```

---

# 3. List Files and Directories

## Basic List
```bash
ls
```

## Detailed List
```bash
ls -l
```

## Show Hidden Files
```bash
ls -la
```

## Explanation
- `-l` → Long listing format
- `-a` → Show hidden files

---

# 4. Change Directory

## Command
```bash
cd directory_name
```

## Example
```bash
cd /etc
```

## Return to Home Directory
```bash
cd
```

## Go Back One Directory
```bash
cd ..
```

---

# 5. Create Files

## Using touch
```bash
touch file1.txt
```

## Create Multiple Files
```bash
touch file1.txt file2.txt file3.txt
```

---

# 6. Create Directories

## Command
```bash
mkdir testfolder
```

## Create Multiple Directories
```bash
mkdir dir1 dir2 dir3
```

## Create Nested Directories
```bash
mkdir -p parent/child/grandchild
```

---

# 7. View File Contents

## Using cat
```bash
cat file1.txt
```

## Using less
```bash
less file1.txt
```

## Using head
```bash
head file1.txt
```

## Using tail
```bash
tail file1.txt
```

## Real-time Log Monitoring
```bash
tail -f /var/log/syslog
```

---

# 8. Edit Files

## Using nano
```bash
nano file1.txt
```

## Using vim
```bash
vim file1.txt
```

---

# 9. Copy Files and Directories

## Copy File
```bash
cp file1.txt backup.txt
```

## Copy Directory
```bash
cp -r testfolder backupfolder
```

## Explanation
- `-r` → Recursive copy

---

# 10. Move and Rename Files

## Move File
```bash
mv file1.txt /home/student/
```

## Rename File
```bash
mv oldname.txt newname.txt
```

---

# 11. Delete Files and Directories

## Remove File
```bash
rm file1.txt
```

## Remove Directory
```bash
rm -r testfolder
```

## Force Delete
```bash
rm -rf testfolder
```

## Warning
`rm -rf` permanently deletes files without confirmation.

---

# 12. Search Files and Directories

## Find File
```bash
find /home -name file1.txt
```

## Find Directory
```bash
find / -type d -name testfolder
```

## Locate Command
```bash
locate file1.txt
```

## Update Locate Database
```bash
sudo updatedb
```

---

# 13. File Permissions

## View Permissions
```bash
ls -l
```

## Example Output
```bash
-rw-r--r-- 1 student student 0 May 10 10:00 file1.txt
```

## Permission Meaning

| Symbol | Meaning |
|---|---|
| r | Read |
| w | Write |
| x | Execute |

---

# 14. Change File Permissions

## Using chmod
```bash
chmod 755 script.sh
```

## Explanation

| Number | Permission |
|---|---|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |

---

# 15. Change File Ownership

## Change Owner
```bash
sudo chown user:user file1.txt
```

## Example
```bash
sudo chown student:student file1.txt
```

---

# 16. Check File Size

## Human Readable Format
```bash
du -h file1.txt
```

## Check Disk Usage
```bash
df -h
```

---

# 17. Compress and Extract Files

## Create tar Archive
```bash
tar -cvf backup.tar testfolder
```

## Extract tar Archive
```bash
tar -xvf backup.tar
```

## Create gzip File
```bash
gzip file1.txt
```

## Extract gzip File
```bash
gunzip file1.txt.gz
```

---

# 18. File Comparison

## Compare Files
```bash
diff file1.txt file2.txt
```

---

# 19. Check File Type

## Command
```bash
file file1.txt
```

## Example Output
```bash
file1.txt: ASCII text
```

---

# 20. Create Symbolic Links

## Command
```bash
ln -s /path/originalfile shortcut
```

## Example
```bash
ln -s /var/log/syslog syslog_link
```

---

# 21. File Management with Wildcards

## Examples

### All TXT Files
```bash
ls *.txt
```

### All Files Starting with "log"
```bash
ls log*
```

### All Files Ending with ".conf"
```bash
ls *.conf
```

---

# 22. Display Hidden Files

Hidden files start with `.`

## Command
```bash
ls -la
```

---

# 23. Monitor Open Files

## Command
```bash
lsof
```

## Example
```bash
sudo lsof /var/log/syslog
```

---

# 24. Archive and Backup Example

## Create Backup Directory
```bash
mkdir backup
```

## Copy Important Files
```bash
cp -r /etc backup/
```

## Compress Backup
```bash
tar -czvf backup.tar.gz backup/
```

---

# Verification

## Verify File Creation
```bash
ls
```

## Verify Permissions
```bash
ls -l
```

## Verify Ownership
```bash
ls -l file1.txt
```

## Verify Compression
```bash
tar -tvf backup.tar
```

---

# Common File Management Commands Summary

| Command | Description |
|---|---|
| `pwd` | Show current directory |
| `ls` | List files |
| `cd` | Change directory |
| `touch` | Create file |
| `mkdir` | Create directory |
| `cp` | Copy files |
| `mv` | Move/Rename files |
| `rm` | Delete files |
| `find` | Search files |
| `chmod` | Change permissions |
| `chown` | Change ownership |
| `tar` | Archive files |
| `gzip` | Compress files |

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

Ubuntu Server 26.04 provides powerful file management tools through the command line. Understanding these commands helps administrators efficiently manage files, directories, permissions, backups, and storage in Linux server environments.



[Linux_File_Permissions_Cheat_Sheet](./asset/Linux_File_Permissions_Cheat_Sheet.pdf)
[ubuntu_file_management](./asset/ubuntu_file_management.pdf)