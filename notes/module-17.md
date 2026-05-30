# File Ownership and Permissions

### File Ownership

Every file has:

- A user owner
- A group owner

By default:
- The user who creates a file becomes the owner.
- The user's primary group becomes the group owner.

Example:

```bash
touch filetest1
ls -l filetest1
```

Output:

```bash
-rw-rw-r-- 1 sysadmin sysadmin 0 Oct 21 10:18 filetest1
```

User owner:
```text
sysadmin
```

Group owner:
```text
sysadmin
```

---

## Viewing User and Group Information

### `id`

Displays:
- UID
- Username
- Primary group
- Supplementary groups

```bash
id
```

Example:

```bash
uid=1001(sysadmin) gid=1001(sysadmin) groups=1001(sysadmin),4(adm),27(sudo)
```

---

### `groups`

Displays only group memberships.

```bash
groups
```

Example:

```bash
sysadmin adm sudo research development
```

---

## Changing the Current Primary Group

### `newgrp`

Temporarily changes your current primary group.

```bash
newgrp groupname
```

Example:

```bash
newgrp research
```

Verify:

```bash
id
```

Exit the temporary shell:

```bash
exit
```

---

## Changing Group Ownership

### `chgrp`

Change the group owner of a file.

```bash
chgrp groupname file
```

Example:

```bash
chgrp research sample
```

Before:

```bash
-rw-rw-r-- 1 sysadmin sysadmin sample
```

After:

```bash
-rw-rw-r-- 1 sysadmin research sample
```

---

### Recursive Group Changes

Change an entire directory tree:

```bash
chgrp -R development test_dir
```

---

## Viewing Detailed File Information

### `stat`

Displays:
- Owner
- Group
- Permissions
- UID/GID
- Timestamps

```bash
stat file
```

Example:

```bash
stat /tmp/filetest1
```

---

## Changing Ownership

### Change User Owner

Root only:

```bash
chown user file
```

Example:

```bash
chown jane filetest1
```

---

### Change User and Group

Root only:

```bash
chown user:group file
```

Example:

```bash
chown jane:users filetest2
```

---

### Change Group Only

Equivalent to `chgrp`.

```bash
chown :group file
```

Example:

```bash
chown :users filetest1
```

---

## File Types

The first character of `ls -l` output indicates file type.

Example:

```bash
-rw-r--r--
```

File type:

```text
-
```

### Common File Types

| Symbol | Type |
|----------|----------|
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |
| `b` | Block device |
| `c` | Character device |
| `p` | Pipe |
| `s` | Socket |

Most commonly encountered:
- Regular files
- Directories
- Symbolic links

---

## Understanding Permissions

Example:

```bash
-rwxr-xr--
```

Breakdown:

```text
- rwx r-x r--
```

| Section | Applies To |
|----------|----------|
| rwx | User owner |
| r-x | Group owner |
| r-- | Others |

---

## Permission Types

### Read (`r`)

For files:
- View contents
- Copy contents

For directories:
- List filenames

---

### Write (`w`)

For files:
- Modify contents

For directories:
- Create files
- Delete files

---

### Execute (`x`)

For files:
- Run as a program

For directories:
- Enter directory (`cd`)
- Access files within it

---

## Directory Permission Rules

### Read on Directory

Allows:

```bash
ls directory
```

View filenames only.

---

### Execute on Directory

Allows:

```bash
cd directory
```

Required to access files inside.

---

### Write on Directory

Allows:
- Create files
- Delete files

Requires execute permission as well.

---

## Permission Precedence

Linux checks permissions in this order:

### Owner

If you own the file:

Use owner permissions only.

---

### Group

If not owner but group member:

Use group permissions only.

---

### Others

If neither owner nor group member:

Use other permissions.

---

## Important Lessons

### Parent Directories Matter

You must have execute permission on every parent directory.

Example:

```text
/data/file.txt
```

Requires:

```text
x on /
x on /data
```

before file permissions are even checked.

---

### File Deletion

Deleting a file depends on:

- Directory permissions
- Not file permissions

Need:

```text
w + x
```

on the directory.

---

### Directory Listing

To run:

```bash
ls directory
```

Need:

```text
r
```

on the directory.

For:

```bash
ls -l directory
```

Need:

```text
r + x
```

---

## Changing Permissions

### `chmod`

Changes file permissions.

```bash
chmod permissions file
```

---

## Symbolic Method

Format:

```text
who operator permissions
```

### Who

| Symbol | Meaning |
|----------|----------|
| u | User |
| g | Group |
| o | Others |
| a | All |

### Operators

| Symbol | Meaning |
|----------|----------|
| + | Add |
| - | Remove |
| = | Set exactly |

### Permission Types

| Symbol | Meaning |
|----------|----------|
| r | Read |
| w | Write |
| x | Execute |

---

### Examples

Add write permission to group:

```bash
chmod g+w file
```

---

Add execute to owner and group:

```bash
chmod ug+x file
```

---

Remove read from others:

```bash
chmod o-r file
```

---

Set owner permissions exactly:

```bash
chmod u=rx file
```

---

## Numeric (Octal) Method

Permission values:

| Value | Permission |
|---------|---------|
| 4 | Read |
| 2 | Write |
| 1 | Execute |

---

### Common Combinations

| Number | Permission |
|----------|----------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 3 | -wx |
| 2 | -w- |
| 1 | --x |
| 0 | --- |

---

### Examples

```bash
chmod 755 script.sh
```

Result:

```text
rwxr-xr-x
```

---

```bash
chmod 754 file
```

Result:

```text
rwxr-xr--
```

---

```bash
chmod 644 file
```

Result:

```text
rw-r--r--
```

---

## Using `stat` to View Permissions

Example:

```bash
stat file
```

Output includes:

```text
Access: (0664/-rw-rw-r--)
```

Shows:
- Numeric permissions
- Symbolic permissions

---

## Umask

### Purpose

Controls default permissions for newly created files and directories.

---

### View Current Umask

```bash
umask
```

Example:

```bash
0002
```

---

## Default Permissions

### Files

Maximum:

```text
666
rw-rw-rw-
```

Files are never created executable by default.

---

### Directories

Maximum:

```text
777
rwxrwxrwx
```

---

## Calculating Umask

Formula:

```text
Default Permissions - Umask
```

Example:

```text
Files:
666 - 027 = 640

Directories:
777 - 027 = 750
```

---

### Example

Set:

```bash
umask 027
```

Create file:

```bash
touch sample
```

Result:

```text
640
rw-r-----
```

---

Create directory:

```bash
mkdir test-dir
```

Result:

```text
750
rwxr-x---
```

---

## Permanent Umask Changes

Modify:

```bash
~/.bashrc
```

Example:

```bash
umask 027
```

Apply changes:

```bash
source ~/.bashrc
```

---

## Common Commands Summary
| Command | Purpose |
|----------|----------|
| `id` | Show UID/GID information |
| `groups` | Show group memberships |
| `newgrp` | Temporarily change primary group |
| `chgrp` | Change group ownership |
| `chown` | Change user/group ownership |
| `stat` | Detailed file information |
| `chmod` | Change permissions |
| `umask` | View/set default permissions |
| `ls -l` | View ownership and permissions |

---

## Best Practices
- Use groups for shared file access.
- Give only necessary permissions.
- Use `755` for directories that need public access.
- Use `644` for normal files.
- Use `600` for sensitive files.
- Be cautious with `777`.
- Remember that directory permissions control access to files inside.
- Verify permissions using `ls -l` or `stat`.
- Set an appropriate `umask` for security.
