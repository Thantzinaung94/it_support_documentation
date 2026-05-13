# Ubuntu Server Group Management Documentation

## Objective

This document explains how to manage groups and users in an Ubuntu Server environment.

The guide includes:

1. Create a group
2. Add a user to a group
3. Display groups assigned to a user
4. Set a default group for a user
5. Remove a user from a group
6. Show all groups and users
7. Check which users belong to a group
8. Delete a group
9. Fix error: cannot remove the primary group of user

---

# Environment

- Operating System: Ubuntu Server 24.04 / 26.04
- Access Method: Terminal / SSH
- Privilege Level: sudo or root access required

---

# 1. Create a Group

## Command

```bash
sudo groupadd groupname
```

## Example

```bash
sudo groupadd developers
```

## Verification

Check whether the group was created successfully:

```bash
getent group developers
```

## Example Output

```bash
developers:x:1002:
```

---

# 2. Add User to the Group

## Command

```bash
sudo usermod -aG groupname username
```

### Explanation

- `-a` = append
- `-G` = supplementary group

## Example

```bash
sudo usermod -aG developers john
```

This command adds user `john` to the `developers` group.

## Verification

```bash
groups john
```

## Example Output

```bash
john : john developers
```

---

# 3. Display Groups Assigned to a User

## Method 1 — Using `groups`

```bash
groups username
```

## Example

```bash
groups john
```

## Output

```bash
john : john developers
```

---

## Method 2 — Using `id`

```bash
id username
```

## Example

```bash
id john
```

## Example Output

```bash
uid=1001(john) gid=1001(john) groups=1001(john),1002(developers)
```

---

# 4. Set Default Group for a User

## Command

```bash
sudo usermod -g groupname username
```

## Example

```bash
sudo usermod -g developers john
```

This command sets `developers` as the primary/default group for user `john`.

## Verification

```bash
id john
```

## Example Output

```bash
uid=1001(john) gid=1002(developers) groups=1002(developers)
```

---

# 5. Remove User from the Group

## Command

```bash
sudo gpasswd -d username groupname
```

## Example

```bash
sudo gpasswd -d john developers
```

## Example Output

```bash
Removing user john from group developers
```

## Verification

```bash
groups john
```

---

# 6. Show All Groups and Users

## Command

```bash
getent group
```

## Example Output

```bash
root:x:0:
sudo:x:27:john
developers:x:1002:
```

### Explanation

- Group Name
- Password Placeholder
- Group ID (GID)
- Group Members

---

## Display Only Group Names

```bash
cut -d: -f1 /etc/group
```

---

# 7. Check Which Users Belong to a Group

## Command

```bash
getent group groupname
```

## Example

```bash
getent group developers
```

## Example Output

```bash
developers:x:1002:john,mike
```

---

## Alternative Method

```bash
grep developers /etc/group
```

---

# 8. Delete a Group

## Command

```bash
sudo groupdel groupname
```

## Example

```bash
sudo groupdel developers
```

This command deletes the `developers` group from the Ubuntu Server.

---

## Verification

Check whether the group still exists:

```bash
getent group developers
```

If there is no output, the group has been deleted successfully.

---

## Important Notes

- A group cannot be deleted if it is the primary/default group of a user.
- Change the user’s primary group before deleting the group.

### Example

```bash
sudo usermod -g users john
sudo groupdel developers
```

---

# 9. Fix Error: cannot remove the primary group of user

## Problem Description

The following error occurs when trying to delete a group:

```bash
groupdel: cannot remove the primary group of user 'hantun'
```

This happens because the group is currently set as the primary/default group for the user `hantun`.

---

# Solution

## Step 1 — Check User Information

Use the following command to verify the user’s current primary group:

```bash
id hantun
```

## Example Output

```bash
uid=1002(hantun) gid=1002(developers) groups=1002(developers)
```

Here:
- `gid=1002(developers)` indicates the primary group.

---

## Step 2 — Change the User’s Primary Group

Set another existing group as the default group.

## Command

```bash
sudo usermod -g users hantun
```

### Explanation

- `-g` changes the primary/default group.
- `users` is the new primary group.
- `hantun` is the username.

---

## Step 3 — Verify the Change

```bash
id hantun
```

## Example Output

```bash
uid=1002(hantun) gid=100(users) groups=100(users),1002(developers)
```

Now the primary group is `users`.

---

## Step 4 — Delete the Group

After changing the primary group, delete the old group:

```bash
sudo groupdel developers
```

---

# Verification

Check whether the group still exists:

```bash
getent group developers
```

If there is no output, the group has been deleted successfully.

---

# Useful Group Management Commands

| Task | Command |
|---|---|
| Create group | `sudo groupadd groupname` |
| Delete group | `sudo groupdel groupname` |
| Add user to group | `sudo usermod -aG groupname username` |
| Remove user from group | `sudo gpasswd -d username groupname` |
| Show user groups | `groups username` |
| Show detailed user info | `id username` |
| Show all groups | `getent group` |

---

# Verification Checklist

| Verification Task | Command |
|---|---|
| Check group exists | `getent group groupname` |
| Check user groups | `groups username` |
| Check default group | `id username` |
| Check all system groups | `getent group` |

---

# Conclusion

This documentation demonstrated essential Ubuntu Server group management tasks including:

- Creating groups
- Managing user memberships
- Setting default groups
- Removing users from groups
- Viewing all groups and memberships
- Deleting groups
- Fixing primary group deletion errors

These commands are commonly used in Linux server administration for permission management and user access control.