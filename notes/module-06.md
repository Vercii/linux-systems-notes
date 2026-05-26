# Linux Documentation and Help Commands

UNIX, the operating system Linux was modeled after, introduced **man pages** (manual pages) to document commands and system features. These pages describe command usage, available options, and additional details.

To open a man page:

```bash
man command
```

Example:

```bash
man ls
```

Use the arrow keys to navigate and press `q` to exit.

---

# Man Pages

Man pages are divided into sections that organize information about a command.

Common sections include:

| Section | Purpose |
|---|---|
| NAME | Command name and short description |
| SYNOPSIS | Command syntax and usage |
| DESCRIPTION | Detailed explanation |
| OPTIONS | Available command options |
| FILES | Related files |
| AUTHOR | Creator of the man page |
| REPORTING BUGS | Bug reporting information |
| COPYRIGHT | License information |
| SEE ALSO | Related documentation |

Example from the `ls` man page:

```text
NAME
    ls - list directory contents
```

---

## Understanding SYNOPSIS

The `SYNOPSIS` section provides a compact command format.

Example:

```text
cal [-31jy] [-A number] [-B number] [-d yyyy-mm] [[month] year]
```

Key syntax symbols:

| Symbol | Meaning |
|---|---|
| `[ ]` | Optional item |
| `...` | Multiple items allowed |
| `|` | Logical OR |

Example:

```text
[-u|--utc|--universal]
```

Means any one of those options may be used.

---

## Searching Inside Man Pages

Search for a term inside a man page:

```text
/search_term
```

Navigation:

- `n` → next result
- `Shift + N` → previous result

---

# Man Page Sections

Linux organizes man pages into numbered sections.

| Section Number | Category |
|---|---|
| 1 | General commands |
| 2 | System calls |
| 3 | Library calls |
| 4 | Special files |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | System administration |
| 9 | Kernel routines |

Example:

```bash
man passwd
```

Displays the section 1 command page:

```text
PASSWD(1)
```

To open the man page for the `passwd` file instead:

```bash
man 5 passwd
```

---

# Finding Man Pages

Use `man -f` or `whatis` to locate matching man pages:

```bash
man -f passwd
```

Example output:

```text
passwd (5) - the password file
passwd (1) - change user password
```

Search descriptions using `man -k` or `apropos`:

```bash
man -k copy
```

Example results:

```text
cp (1) - copy files and directories
scp (1) - secure copy
```

---

# The `whereis` Command

`whereis` searches for commands, source files, and man pages.

Example:

```bash
whereis ls
```

Output:

```text
ls: /bin/ls /usr/share/man/man1/ls.1.gz
```

Compressed man pages usually end with `.gz`.

---

# The `locate` Command

The `locate` command searches a database of files and directories.

Example:

```bash
locate gshadow
```

The database is typically updated nightly, so recently created files may not appear immediately.

Useful options:

| Option | Purpose |
|---|---|
| `-c` | Count matching results |
| `-b` | Match only basenames |

Examples:

```bash
locate -c passwd
locate -b "\passwd"
```

The backslash `\` forces an exact basename match.

---

# Info Documentation

The `info` command provides structured, book-style documentation.

Unlike man pages, info documentation is interconnected using menus and hyperlinks.

Open an info page:

```bash
info command
```

Example:

```bash
info ls
```

Info documents are divided into **nodes**, similar to chapters in a book.

Navigation keys:

| Key | Function |
|---|---|
| `q` | Quit |
| `h` | Tutorial |
| `TAB` | Next hyperlink |
| `ENTER` | Follow hyperlink |
| `u` | Go up one level |
| `l` | Return to previous node |

Example menu:

```text
* Sorting the output::
* Formatting file timestamps::
```

Selecting a menu item opens another node with more detailed information.

---

# Using `--help`

Many commands provide quick help using the `--help` option.

Example:

```bash
cat --help
```

This displays:

- Command usage
- Available options
- Examples
- Documentation references

The `--help` option is useful for quickly checking syntax without opening full documentation.

---

# What I learned

- `man` displays manual pages for commands and system features
- `man -f` / `whatis` finds matching man pages
- `man -k` / `apropos` searches descriptions by keyword
- `whereis` locates commands and their man pages
- `locate` searches the filesystem database
- `info` provides structured, linked documentation
- `command --help` gives quick command usage information
