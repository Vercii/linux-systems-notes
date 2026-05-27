# Linux Archiving and Compression

Archiving and compression are used to store and transfer files more efficiently.

## Key Concepts

- **Archiving** combines multiple files into a single file.
- **Compression** reduces file size by removing redundant data.
- **Un-archiving** extracts files from an archive.

Files may be compressed individually or archived first and then compressed.

---

# Why Archiving and Compression Matter

Even with cheap storage, archiving and compression are still important because they:

- Reduce storage space usage
- Speed up file transfers
- Simplify backups
- Organize multiple files into one package
- Help manage large log files
- Improve performance on slower networks or tape storage

---

# Compression Types

## Lossless Compression

- No information is lost
- Decompressed files are identical to the original
- Used for:
  - Documents
  - Logs
  - Software
  - Archives

Examples:
- `gzip`
- `bzip2`
- `xz`
- PNG and GIF images

---

## Lossy Compression

- Some data is permanently removed
- Smaller file sizes but slightly reduced quality
- Commonly used for media

Examples:
- JPEG images
- MP3 audio

Repeated lossy compression reduces quality over time.

---

# The `gzip` Command

`gzip` compresses files using the Lempel-Ziv algorithm.

Syntax:

```bash
gzip filename
```

Example:

```bash
gzip longfile.txt
```

Before compression:

```bash
-rw-r--r-- 1 sysadmin sysadmin 66540 longfile.txt
```

After compression:

```bash
-rw-r--r-- 1 sysadmin sysadmin 341 longfile.txt.gz
```

The original file is replaced with the compressed version.

---

# Viewing Compression Information

Use `-l` to display compression details:

```bash
gzip -l longfile.txt.gz
```

Example output:

```bash
compressed  uncompressed  ratio
341         66540         99.5%
```

---

# Decompressing Files

Use either:

```bash
gunzip filename.gz
```

or:

```bash
gzip -d filename.gz
```

Example:

```bash
gunzip longfile.txt.gz
```

The original file is restored.

---

# Other Compression Utilities

## `bzip2`

Uses the Burrows-Wheeler algorithm.

Commands:

```bash
bzip2 file
bunzip2 file.bz2
```

Extensions:

```text
.bz
.bz2
```

Usually compresses better than `gzip`, but uses more CPU time.

---

## `xz`

Uses the LZMA algorithm.

Commands:

```bash
xz file
unxz file.xz
```

Extension:

```text
.xz
```

Provides high compression with efficient decompression.

---

# The `tar` Command

`tar` archives multiple files into one file called a **tarball**.

Main modes:

| Mode | Function |
|---|---|
| `-c` | Create archive |
| `-t` | List archive contents |
| `-x` | Extract archive |

---

# Creating Archives

Syntax:

```bash
tar -cf archive.tar files
```

Example:

```bash
tar -cf alpha_files.tar alpha*
```

Options:

| Option | Meaning |
|---|---|
| `-c` | Create archive |
| `-f` | Specify archive filename |

---

# Creating Compressed Archives

## Using `gzip`

```bash
tar -czf archive.tar.gz files
```

Example:

```bash
tar -czf alpha_files.tar.gz alpha*
```

Option:

| Option | Meaning |
|---|---|
| `-z` | Compress using gzip |

---

## Using `bzip2`

```bash
tar -cjf archive.tar.bz2 files
```

Example:

```bash
tar -cjf folders.tbz School
```

Option:

| Option | Meaning |
|---|---|
| `-j` | Compress using bzip2 |

---

# Common Archive Extensions

| Extension | Description |
|---|---|
| `.tar` | Archive only |
| `.tar.gz` / `.tgz` | gzip-compressed archive |
| `.tar.bz2` / `.tbz` | bzip2-compressed archive |
| `.xz` | xz-compressed file |

---

# Listing Archive Contents

## gzip archive

```bash
tar -tzf archive.tar.gz
```

## bzip2 archive

```bash
tar -tjf archive.tar.bz2
```

Example:

```bash
tar -tjf folders.tbz
```

Output:

```text
School/
School/Engineering/
School/Art/
School/Math/
```

---

# Extracting Archives

## gzip archive

```bash
tar -xzf archive.tar.gz
```

## bzip2 archive

```bash
tar -xjf archive.tar.bz2
```

Example:

```bash
tar -xjf folders.tbz
```

Options:

| Option | Meaning |
|---|---|
| `-x` | Extract archive |
| `-j` | Use bzip2 |
| `-z` | Use gzip |
| `-f` | Specify archive file |

---

# Verbose Extraction

Use `-v` to show extracted files:

```bash
tar -xjvf folders.tbz
```

Example output:

```text
School/
School/Engineering/
School/Art/
```

---

# Extracting Specific Files

Extract only one file:

```bash
tar -xjvf folders.tbz School/Art/linux.txt
```

Only matching files are extracted.

---

# Important `tar` Note

The `-f` option must come last among grouped options because the next argument is treated as the archive filename.

Correct:

```bash
tar -xjvf archive.tbz
```

Incorrect:

```bash
tar -xjfv archive.tbz
```

---

# The `zip` Command

ZIP archives are common on Windows systems.

Syntax:

```bash
zip archive.zip files
```

Example:

```bash
zip alpha_files.zip alpha*
```

Unlike `tar`, ZIP archives are automatically compressed.

---

# Recursive ZIP Archives

`zip` does not recurse into directories by default.

Use `-r`:

```bash
zip -r School.zip School
```

This includes all files and subdirectories.

---

# Listing ZIP Contents

Use `unzip -l`:

```bash
unzip -l School.zip
```

Displays archived files without extracting them.

---

# Extracting ZIP Archives

Extract all files:

```bash
unzip School.zip
```

Extract a specific file:

```bash
unzip School.zip School/Math/numbers.txt
```

Extract files using patterns:

```bash
unzip School.zip School/Art/*t
```

---

# ZIP Extraction Prompts

If files already exist:

```text
replace file? [y]es [n]o [A]ll [N]one [r]ename
```

To avoid conflicts, extract archives into a new directory.

Example:

```bash
mkdir tmp
cp School.zip tmp/
cd tmp
unzip School.zip
```

---

# Key Takeaways

- Compression reduces file sizes
- Archiving combines multiple files into one
- `gzip`, `bzip2`, and `xz` are common compression tools
- `tar` creates and extracts archives
- `tar -czf` creates gzip-compressed archives
- `tar -cjf` creates bzip2-compressed archives
- `zip` creates ZIP archives
- `unzip` extracts ZIP archives
- `-v` enables verbose output
- `-r` enables recursive directory handling
