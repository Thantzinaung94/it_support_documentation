# VI(vim) Text Editor Cheat Sheet

## VI Modes

### Command Mode (Default)
Used for commands and navigation.

### Insert Mode
Used for text editing.  
Enter Insert Mode by pressing:

```bash
i
```

---

# Opening and Closing Files

## Open a File

```bash
vi <filename>
```

## Save and Exit

```bash
:wq
```

## Save Without Exiting

```bash
:w
```

## Exit Without Saving

```bash
:q!
```

---

# Basic Navigation

## Move Cursor

| Key | Action |
|---|---|
| `h` | Move Left |
| `l` | Move Right |
| `j` | Move Down |
| `k` | Move Up |

## Jump to Beginning of File

```bash
gg
```

## Jump to End of File

```bash
G
```

## Jump to a Specific Line

```bash
:<line_number>
```

Example:

```bash
:25
```

---

# Insert Mode

## Enter Insert Mode

```bash
i
```

## Exit Insert Mode

Press:

```bash
Esc
```

---

# Editing Commands

## Delete a Character

```bash
x
```

## Delete a Whole Line

```bash
dd
```

## Copy a Line

```bash
yy
```

## Paste Copied or Cut Content

```bash
p
```

## Replace a Character

```bash
r<character>
```

Example:

```bash
ra
```

## Undo Last Change

```bash
u
```

## Redo Undone Change

```bash
Ctrl + r
```

---

# Searching

## Search for a Word

```bash
/<word>
```

Example:

```bash
/hello
```

## Search Backward

```bash
?<word>
```

## Move to Next Occurrence

```bash
n
```

## Move to Previous Occurrence

```bash
N
```

---

# Advanced Editing

## Delete from Cursor to End of Line

```bash
D
```

## Delete from Cursor to Beginning of Line

```bash
d0
```

## Change a Word

```bash
cw
```

## Replace the Entire Line

```bash
cc
```

---

# Visual Mode

## Enter Visual Mode

```bash
v
```

## Highlight Text

Use:

```bash
h, j, k, l
```

or arrow keys.

## Copy Highlighted Text

```bash
y
```

## Delete Highlighted Text

```bash
d
```

---

# File Management

## Open a New File

```bash
:e <filename>
```

## Save File with a New Name

```bash
:w <new_filename>
```

## Quit All Files

```bash
:qa
```

---

# Useful Tips

- Practice using `u` and `Ctrl + r` for undo and redo.
- Start with test files before editing important system files.
- Use Visual Mode for easier text selection.
- Always create backups before editing critical configuration files.
- Press `Esc` anytime to safely return to Command Mode.

---

# Quick Reference Table

| Command | Description |
|---|---|
| `i` | Insert Mode |
| `Esc` | Command Mode |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and Quit |
| `:q!` | Quit Without Saving |
| `dd` | Delete Line |
| `yy` | Copy Line |
| `p` | Paste |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `/word` | Search |
| `gg` | Top of File |
| `G` | Bottom of File |

![vi_text_editer_chet_sheet](./asset/image/)