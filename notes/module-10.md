# Linux Text Processing, Redirection, Pipes, and Regular Expressions

This chapter focuses on how Linux handles **text files**, how commands can process text, and how command output can be redirected or combined with other commands. Since Linux systems rely heavily on text-based configuration and log files, these tools are essential for administration and automation.

---

# 1. Viewing and Managing Text Files

## `cat` Command

The `cat` command (short for *concatenate*) is commonly used to:

- Display file contents
- Create text files
- Combine files

### Display a File

```bash
cat food.txt
```

Example output:

```bash
Food is good.
```

---

# 2. Viewing Large Files with Pagers

Using `cat` on large files floods the terminal. Linux provides pager tools:

| Command | Purpose |
|---|---|
| `less` | Advanced pager |
| `more` | Older/simple pager |

---

## Using `less`

```bash
less words
```

Useful navigation keys:

| Key | Action |
|---|---|
| Space | Next page |
| B | Previous page |
| Enter | Next line |
| Q | Quit |
| H | Help |

---

# 3. `head` and `tail`

These commands display portions of files.

---

## `head`

Displays first 10 lines by default:

```bash
head /etc/sysctl.conf
```

### Show First 3 Lines

```bash
head -n 3 /etc/sysctl.conf
```

---

## `tail`

Displays last 10 lines by default:

```bash
tail /etc/sysctl.conf
```

### Show Last 5 Lines

```bash
tail -5 /etc/sysctl.conf
```

---

## Live Monitoring with `tail -f`

Useful for logs:

```bash
tail -f /var/log/mail.log
```

This continuously watches file updates in real time.

---

# 4. Pipes (`|`)

Pipes send the output of one command into another command.

Syntax:

```bash
command1 | command2
```

---

## Example: View First 10 Entries

```bash
ls /etc | head
```

Flow:

```text
ls output → head input
```

---

## Multiple Pipes

```bash
ls /etc/ssh | nl | tail -5
```

Process:

1. `ls` lists files
2. `nl` adds line numbers
3. `tail -5` shows last 5 lines

---

## Pipe Order Matters

### Example 1

```bash
ls /etc/ssh | nl | tail -5
```

Numbers all lines first.

### Example 2

```bash
ls /etc/ssh | tail -5 | nl
```

Only numbers the last 5 lines.

---

# 5. Standard Streams

Linux commands use 3 streams:

| Stream | Name | Number |
|---|---|---|
| STDIN | Standard Input | 0 |
| STDOUT | Standard Output | 1 |
| STDERR | Standard Error | 2 |

---

# 6. Redirecting Output

## Redirect STDOUT (`>`)

```bash
echo "Line 1" > example.txt
```

Creates or overwrites file.

---

## Append Output (`>>`)

```bash
echo "Another line" >> example.txt
```

Adds content without overwriting.

---

# 7. Redirecting STDERR

## Redirect Errors Only

```bash
ls /fake 2> error.txt
```

Error goes into `error.txt`.

---

## Redirect STDOUT and STDERR Together

```bash
ls /fake /etc/ppp &> all.txt
```

Both outputs go into one file.

---

## Redirect Separately

```bash
ls /fake /etc/ppp > output.txt 2> error.txt
```

| Stream | Destination |
|---|---|
| STDOUT | output.txt |
| STDERR | error.txt |

---

# 8. Redirecting STDIN (`<`)

Some commands read input from keyboard unless redirected.

---

## Example with `tr`

### Keyboard Input

```bash
tr 'a-z' 'A-Z'
```

Input:

```text
hello
```

Output:

```text
HELLO
```

---

## Redirect File into Command

```bash
tr 'a-z' 'A-Z' < example.txt
```

---

## Redirect Input and Output Together

```bash
tr 'a-z' 'A-Z' < example.txt > newexample.txt
```

---

# 9. `sort` Command

Sorts text alphabetically or numerically.

---

## Alphabetical Sort

```bash
sort mypasswd
```

---

## Numeric Sort by Field

```bash
sort -t: -n -k3 mypasswd
```

Options:

| Option | Meaning |
|---|---|
| `-t:` | Colon delimiter |
| `-n` | Numeric sort |
| `-k3` | Sort by field 3 |

---

## Reverse Sort

```bash
sort -t: -n -r -k3 mypasswd
```

---

## Multi-Field Sort

```bash
sort -t, -k2 -k1n -k3 os.csv
```

Sort order:

1. Field 2
2. Numeric field 1
3. Field 3

---

# 10. `wc` Command

Counts:

- Lines
- Words
- Bytes

---

## Example

```bash
wc /etc/passwd
```

---

## Count Files in Directory

```bash
ls /etc | wc -l
```

---

# 11. `cut` Command

Extracts fields or character positions.

---

## Extract Fields

```bash
cut -d: -f1,5-7 mypasswd
```

| Option | Meaning |
|---|---|
| `-d:` | Colon delimiter |
| `-f` | Select fields |

---

## Extract Character Positions

```bash
ls -l | cut -c1-11,50-
```

---

# 12. `grep` Command

Searches text using patterns.

---

## Basic Search

```bash
grep bash /etc/passwd
```

---

## Useful `grep` Options

| Option | Function |
|---|---|
| `-c` | Count matches |
| `-n` | Show line numbers |
| `-v` | Invert match |
| `-i` | Ignore case |
| `-w` | Match whole words |

---

## Examples

### Count Matches

```bash
grep -c bash /etc/passwd
```

### Ignore Case

```bash
grep -i the newhome.txt
```

### Whole Word Only

```bash
grep -w are newhome.txt
```

---

# 13. Regular Expressions (Regex)

Regex allows advanced pattern matching.

---

# Basic Regex Characters

| Symbol | Meaning |
|---|---|
| `.` | Any single character |
| `[ ]` | Character list/range |
| `*` | Previous character repeated 0+ times |
| `^` | Beginning of line |
| `$` | End of line |

---

# 14. Period (`.`)

Matches any single character.

Example:

```bash
grep 'r..f' red.txt
```

Matches:

```text
reef
roof
```

---

# 15. Character Sets `[ ]`

## Match Digits

```bash
grep '[0-9]' profile.txt
```

---

## Match Ranges

```bash
grep '[a-z]' file.txt
```

---

## Negated Sets

```bash
grep '[^0-9]' profile.txt
```

Matches lines containing non-numbers.

---

# 16. Asterisk (`*`)

Matches zero or more of previous pattern.

Example:

```bash
grep 're*d' red.txt
```

Matches:

```text
red
reeed
rd
reed
```

---

# 17. Anchors

## Beginning of Line `^`

```bash
grep '^root' /etc/passwd
```

---

## End of Line `$`

```bash
grep 'r$' alpha-first.txt
```

---

# 18. Escaping Special Characters

Use backslash `\` to search literal regex symbols.

Example:

```bash
grep 're\*' newhome.txt
```

---

# 19. Extended Regular Expressions

Use:

```bash
grep -E
```

---

## Extended Regex Symbols

| Symbol | Meaning |
|---|---|
| `?` | Optional character |
| `+` | One or more |
| `|` | OR |

---

## Examples

### Optional Character

```bash
grep -E 'colou?r' spelling.txt
```

Matches:

```text
color
colour
```

---

### One or More

```bash
grep -E 'e+' red.txt
```

---

### OR Operator

```bash
grep -E 'gray|grey' spelling.txt
```

---

# Key Concepts

| Topic | Purpose |
|---|---|
| `cat` | Display/create text |
| `less` | View large files |
| `head`/`tail` | View beginning/end |
| Pipes `|` | Chain commands |
| Redirection `>` `<` | Control streams |
| `sort` | Rearrange text |
| `wc` | Count lines/words |
| `cut` | Extract columns |
| `grep` | Search patterns |
| Regex | Advanced matching |

---

# Important Exam/Lab Commands

```bash
cat file.txt
less file.txt
head -n 5 file.txt
tail -f logfile
ls | head
echo "text" > file.txt
echo "text" >> file.txt
command 2> error.txt
command &> all.txt
sort -t: -n -k3 file
wc -l file
cut -d: -f1 file
grep pattern file
grep -E 'a|b' file
```
