# Linux File Management and Globbing

When working in Linux, it is important to know how to manage files and directories from the command line. Linux is also completely **case-sensitive**, meaning:

```bash
hello.txt
HELLO.txt
Hello.txt
```

are all different files.

Linux uses the **UTF-8** character standard, based on ASCII.

---

# Globbing (Wildcards)

Glob characters, also called wildcards, allow pattern matching for filenames. These patterns are interpreted by the shell before commands are executed.

Common glob characters:

| Character | Meaning |
|---|---|
| `*` | Zero or more characters |
| `?` | Exactly one character |
| `[ ]` | Character range or set |
| `[! ]` | Negated range |

The `echo` command is commonly used to demonstrate glob expansion.

---

## Asterisk (`*`)

Matches zero or more characters.

Example:

```bash
echo /etc/t*
```

Matches all files in `/etc` beginning with `t`.

Match all files ending in `.d`:

```bash
echo /etc/*.d
```

Match files beginning with `r` and ending with `.conf`:

```bash
echo /etc/r*.conf
```

---

## Question Mark (`?`)

Matches exactly one character.

Example:

```bash
echo /etc/t???????
```

Matches files beginning with `t` followed by exactly seven characters.

Find files with three-letter extensions:

```bash
echo /etc/*.???
```

---

## Brackets (`[ ]`)

Match one character from a set or range.

Example:

```bash
echo /etc/[gu]*
```

Matches files beginning with `g` or `u`.

Character ranges:

```bash
echo /etc/[a-d]*
```

Matches files beginning with letters between `a` and `d`.

Find filenames containing numbers:

```bash
echo /etc/*[0-9]*
```

---

## Negated Ranges (`[! ]`)

Exclude characters from matching.

Example:

```bash
echo /etc/[!a-t]*
```

Matches files not beginning with letters `a` through `t`.

---

# Important Note About `ls` and Globs

The shell expands glob patterns before commands execute.

Example:

```bash
ls /etc/a*
```

is expanded internally into:

```bash
ls /etc/adduser.conf /etc/alternatives /etc/apparmor
```

If a matched item is a directory, `ls` displays the directory contents instead of the directory name.

Example:

```bash
ls /etc/ap*
```

may show directory contents rather than just names.

To force `ls` to display directory names only, use:

```bash
ls -d /etc/x*
```

---

# The `cp` Command

The `cp` command copies files and directories.

Syntax:

```bash
cp source destination
```

Copy a file into the home directory:

```bash
cp /etc/hosts ~
```

Verbose output:

```bash
cp -v /etc/hosts ~
```

Rename while copying:

```bash
cp /etc/hosts ~/hosts.copy
```

---

# Preventing Overwrites

By default, `cp` overwrites existing files.

## Interactive Mode (`-i`)

Prompt before overwriting:

```bash
cp -i /etc/hosts example.txt
```

## No Clobber (`-n`)

Prevent overwriting automatically:

```bash
cp -n /etc/skel/.* ~
```

---

# Copying Directories

Use recursive mode:

```bash
cp -r source_directory destination_directory
```

Example:

```bash
cp -r Documents Backup
```

Both `-r` and `-R` perform recursive copying.

---

# The `mv` Command

The `mv` command moves or renames files.

Syntax:

```bash
mv source destination
```

Move a file:

```bash
mv hosts Videos
```

Rename a file:

```bash
mv newexample.txt myfile.txt
```

Move and rename simultaneously:

```bash
mv example.txt Videos/newexample.txt
```

---

# Useful `mv` Options

| Option | Meaning |
|---|---|
| `-i` | Interactive overwrite prompt |
| `-n` | No overwrite |
| `-v` | Verbose output |

Unlike `cp`, the `mv` command does not require `-r` for directories.

---

# The `touch` Command

The `touch` command creates empty files.

Example:

```bash
touch sample
```

Verify file creation:

```bash
ls -l sample
```

Example output:

```bash
-rw-rw-r-- 1 sysadmin sysadmin 0 Nov 9 16:48 sample
```

The file size is `0` bytes because the file is empty.

---

# The `rm` Command

The `rm` command deletes files.

Example:

```bash
rm sample
```

Delete multiple files:

```bash
rm hosts.copy
```

Warning: Deleted files are permanently removed.

---

# Interactive Deletion

Use `-i` to confirm deletion:

```bash
rm -i *.txt
```

Example prompts:

```bash
rm: remove regular empty file `example.txt'?
```

---

# Removing Directories

By default, `rm` cannot remove directories.

Example:

```bash
rm Videos
```

Output:

```bash
rm: cannot remove 'Videos': Is a directory
```

Use recursive deletion:

```bash
rm -r Videos
```

Be careful — all files and subdirectories are deleted.

---

# The `rmdir` Command

`rmdir` removes only empty directories.

Example:

```bash
rmdir Documents
```

If the directory is not empty:

```bash
rmdir: failed to remove 'Documents': Directory not empty
```

---

# The `mkdir` Command

The `mkdir` command creates directories.

Example:

```bash
mkdir test
```

Verify creation:

```bash
ls
```

---

# What I learned
- Linux filenames are case-sensitive
- Globs allow filename pattern matching
- `*` matches many characters
- `?` matches one character
- `[ ]` matches character ranges
- `cp` copies files and directories
- `mv` moves or renames files
- `touch` creates empty files
- `rm` deletes files
- `rm -r` deletes directories recursively
- `rmdir` removes empty directories
- `mkdir` creates directories
