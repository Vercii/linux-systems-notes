# Linux Filesystem and Navigation

In Linux, everything is considered a file. Files store data such as text, graphics, and programs, while directories are special files used to store other files. Windows and macOS users typically refer to directories as folders.

Understanding how to navigate and manage files from the command line is an essential Linux skill.

---

# Linux Filesystem Structure

Windows uses drive letters like `C:` or `D:` under **My Computer**. Linux works differently.

The top level of the Linux filesystem is called the **root directory**, represented by:

```bash
/
```

Instead of drive letters, physical devices are mounted within the filesystem under directories.

---

# Home Directory

Most Linux systems contain a `/home` directory.

Inside `/home` is a separate directory for each user.

Example:

```bash
/home/sysadmin
```

This is the home directory for the `sysadmin` user.

The home directory is important because:

- Users usually begin there when opening a shell
- Users typically store personal files there
- Users usually have full control over files inside their home directory

The home directory is represented by the tilde symbol:

```bash
~
```

Examples:

```bash
~
/home/sysadmin
```

Both represent the same location for the current user.

Another user's home directory can be referenced using:

```bash
~username
```

Example:

```bash
~bob
```

Equivalent to:

```bash
/home/bob
```

---

# The `pwd` Command

The `pwd` command displays the current working directory.

Syntax:

```bash
pwd
```

Example:

```bash
sysadmin@localhost:~$ pwd
/home/sysadmin
```

---

# The `cd` Command

The `cd` command changes directories.

Syntax:

```bash
cd [path]
```

Move into a directory:

```bash
cd Documents
```

Return to the home directory:

```bash
cd
```

If the directory does not exist, Bash displays an error:

```bash
cd Junk
```

Output:

```bash
-bash: cd: Junk: No such file or directory
```

---

# Paths in Linux

A path is a list of directories separated by `/`.

Example:

```bash
/home/sysadmin
```

There are two types of paths:

| Path Type | Description |
|---|---|
| Absolute Path | Starts from the root `/` |
| Relative Path | Starts from the current directory |

---

## Absolute Paths

Absolute paths always begin with `/`.

Example:

```bash
cd /home/sysadmin/Documents
```

---

## Relative Paths

Relative paths begin from the current directory.

Example:

```bash
cd Documents
cd School/Art
```

If currently inside `Documents`, the command:

```bash
cd School/Art
```

moves into the `Art` directory inside `School`.

Verify location:

```bash
pwd
```

---

# Special Directory Symbols

| Symbol | Meaning |
|---|---|
| `.` | Current directory |
| `..` | Parent directory |
| `~` | Home directory |

Move one directory up:

```bash
cd ..
```

Move up two levels and into Downloads:

```bash
cd ../../Downloads
```

---

# The `ls` Command

The `ls` command lists directory contents.

Syntax:

```bash
ls [OPTION]... [FILE]...
```

Basic usage:

```bash
ls
```

Example output:

```bash
Desktop  Documents  Downloads  Music  Pictures
```

List another directory:

```bash
ls /var
```

---

# Hidden Files

Files beginning with `.` are hidden.

Display hidden files using:

```bash
ls -a
```

Example output:

```bash
.bashrc
.profile
.cache
```

Hidden files are commonly configuration files.

---

# Long Listing Format (`-l`)

Use `-l` to display detailed file information:

```bash
ls -l
```

Example:

```bash
-rw-r--r-- 1 root root 15322 Dec 10 21:33 alternatives.log
```

Fields shown:

| Field | Description |
|---|---|
| File Type | Directory, file, link, etc. |
| Permissions | Access permissions |
| Link Count | Number of hard links |
| Owner | File owner |
| Group | Group owner |
| Size | File size |
| Timestamp | Last modified time |
| Filename | File name |

---

# File Types

| Symbol | File Type |
|---|---|
| `d` | Directory |
| `-` | Regular file |
| `l` | Symbolic link |
| `s` | Socket |
| `p` | Pipe |
| `b` | Block device |
| `c` | Character device |

Example:

```bash
drwxr-xr-x
```

The leading `d` means directory.

---

# Human-Readable File Sizes

Use `-h` with `-l` for readable file sizes:

```bash
ls -lh
```

Example:

```bash
-rw-rw-r-- 1 root utmp 286K Dec 15 16:38 lastlog
```

---

# Listing the Current Directory Itself

The `-d` option lists the directory itself instead of its contents.

Example:

```bash
ls -ld
```

Output:

```bash
drwxr-xr-x 1 sysadmin sysadmin 224 Nov 7 17:07 .
```

---

# Recursive Listings

Use `-R` to list files recursively through subdirectories.

Example:

```bash
ls -R /etc/ppp
```

Be careful when using recursive listings on large directories.

---

# Sorting `ls` Output

## Sort by Size

```bash
ls -lS
```

Largest files appear first.

Human-readable version:

```bash
ls -lSh
```

---

## Sort by Modification Time

```bash
ls -lt
```

Most recently modified files appear first.

Display full timestamps:

```bash
ls -t --full-time
```

---

## Reverse Sorting

Use `-r` to reverse sorting order.

Sort smallest to largest:

```bash
ls -lrS
```

Sort oldest to newest:

```bash
ls -lrt
```

---

# Important Notes About `ls`

Many Linux systems automatically colorize `ls` output using aliases.

Check the alias:

```bash
type ls
```

Example:

```bash
ls is aliased to `ls --color=auto'
```

Bypass the alias:

```bash
\ls
```

---

# What I learned
- Linux uses a hierarchical filesystem beginning at `/`
- User home directories are usually stored in `/home`
- `pwd` shows the current directory
- `cd` changes directories
- Absolute paths start with `/`
- Relative paths start from the current directory
- `.` represents the current directory
- `..` represents the parent directory
- `ls` lists files and directories
- `ls -l` shows detailed metadata
- `ls -a` displays hidden files
- `ls -R` performs recursive listings
- `ls -S`, `-t`, and `-r` change sorting behavior
