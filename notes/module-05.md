# Module 5 - Command Line Skills

## Linux Shell and Bash

After a user enters a command, the terminal sends it to the shell, which interprets the command and tells the operating system what to do. If the command succeeds, output is displayed in the terminal; otherwise, the shell shows an error message.

Linux supports many different shells, but the most commonly used is **Bash** (Bourne Again Shell). Bash includes features such as command history, inline editing, scripting, aliases, and variables.

---

## Shell Prompt

When Bash starts, it displays a prompt indicating it is ready for commands.

Example:

```bash
sysadmin@localhost:~$
```

Prompt components:

- `sysadmin` → username
- `localhost` → system name
- `~` → current directory (home directory)

Example home directory:

```bash
/home/sysadmin
```

---

## Linux Commands

Commands generally follow this format:

```bash
command [options] [arguments]
```

- **Arguments** specify what the command acts on.
- **Options** modify command behavior.

Examples:

```bash
ls /etc/ppp
ls /etc/ppp /etc/ssh
ls -l
```

Common `ls` options:

- `-l` → long listing format
- `-r` → reverse order
- `-h` → human-readable file sizes

Options can be combined:

```bash
ls -lr
ls -rl
```

Linux is **case-sensitive**, so capitalization matters for commands, filenames, variables, and options.

Options may use short or long formats:

```bash
-h
--human-readable
```

---

## Command History

Bash stores previously executed commands in a history list.

| Command | Function |
|---|---|
| `history` | Show command history |
| `!!` | Repeat last command |
| `!3` | Run command #3 |
| `!-3` | Run third command from bottom |
| `!ls` | Run most recent `ls` command |

Arrow keys can also navigate and edit command history.

---

## Variables and Environment Variables

### Local Variables

Local variables exist only in the current shell session.

Create a variable:

```bash
variable1='Something'
```

Display its value:

```bash
echo $variable1
```

Local variables disappear when the shell closes.

---

### Environment Variables

Environment variables are available system-wide.

Common environment variables:

- `PATH`
- `HOME`
- `HISTSIZE`

View a variable:

```bash
echo $HISTSIZE
```

Display all environment variables:

```bash
env
```

Export a local variable:

```bash
export variable1
```

Create and export simultaneously:

```bash
export variable2='Else'
```

Remove a variable:

```bash
unset variable2
```

---

## PATH Variable

`PATH` stores directories Bash searches for commands.

Example:

```bash
echo $PATH
```

Directories are separated by `:`.

Example path:

```bash
/home/sysadmin
```

If a command is not found in any directory listed in `PATH`, Bash returns:

```bash
command not found
```

Add a custom directory to `PATH`:

```bash
PATH=/usr/bin/custom:$PATH
```

Always include the existing `$PATH` value when modifying it.

---

## Command Types

The `type` command identifies how Bash interprets a command.

Syntax:

```bash
type command
```

Commands can be:

- Built-in commands
- External commands
- Aliases
- Functions

Example:

```bash
type cd
```

Output:

```bash
cd is a shell builtin
```

---

## External Commands

External commands are executable files stored in directories listed in `PATH`.

Find a command location:

```bash
which ls
```

Example output:

```bash
/bin/ls
```

Commands can also be executed directly using their full path:

```bash
/ bin / ls
```

Show all matching command locations:

```bash
type -a echo
```

---

## Aliases

Aliases are shortcuts for longer commands.

Examples:

```bash
ll='ls -alF'
l='ls -CF'
```

View aliases:

```bash
alias
```

Create an alias:

```bash
alias mycal="cal 2019"
```

Aliases are temporary and disappear when the shell closes.

---

## Functions

Functions are reusable blocks of commands.

Example:

```bash
my_report ()
{
   ls Documents
   date
   echo "Document directory report"
}
```

Run the function like a normal command:

```bash
my_report
```

Functions are commonly used in scripts and automation.

---

# Bash Quotation Marks and Command Substitution

## Quote Types

| Quote Type | Symbol | Purpose |
|---|---|---|
| Double Quotes | `"` | Prevents interpretation of most special characters |
| Single Quotes | `'` | Prevents interpretation of all special characters |
| Backticks | `` ` ` `` | Performs command substitution |

---

## Double Quotes (`"`)

Double quotes prevent wildcard expansion but still allow variable and command substitution.

Example:

```bash
echo "The path is $PATH"
```

---

## Single Quotes (`'`)

Single quotes treat everything literally.

Example:

```bash
echo 'The car costs $100'
```

Without single quotes:

```bash
echo The car costs $100
```

Bash interprets `$1` as a variable, resulting in incorrect output.

---

## Escaping Characters (`\`)

A backslash escapes a single character.

Example:

```bash
echo The service costs \$1 and the path is $PATH
```

- `\$1` is treated literally
- `$PATH` is still expanded

---

## Command Substitution

Backticks execute a command and insert its output.

Example:

```bash
echo Today is `date`
```

Modern Bash usually uses:

```bash
echo Today is $(date)
```

This syntax is cleaner and easier to read.

---

## Globbing (Wildcards)

Common wildcard characters:

| Character | Meaning |
|---|---|
| `*` | Matches many characters |
| `?` | Matches one character |
| `[ ]` | Matches a range/set |

Example:

```bash
ls *.txt
```

Lists all `.txt` files.

---

# Bash Control Statements

Control statements allow commands to run sequentially or conditionally.

---

## Semicolon (`;`)

Runs commands sequentially regardless of success or failure.

```bash
command1; command2; command3
```

Example:

```bash
date; whoami; pwd
```

---

## Logical AND (`&&`)

Runs the second command only if the first succeeds.

```bash
command1 && command2
```

Example:

```bash
ls /etc/ppp && echo success
```

---

## Logical OR (`||`)

Runs the second command only if the first fails.

```bash
command1 || command2
```

Example:

```bash
ls /etc/junk || echo failed
```

---

## Exit Status

Commands return an exit status:

| Exit Code | Meaning |
|---|---|
| `0` | Success |
| Non-zero | Failure |

`&&` and `||` rely on these exit codes.

---

## Comparison Table

| Operator | Meaning | Second Command Runs When |
|---|---|---|
| `;` | Sequential execution | Always |
| `&&` | Logical AND | First command succeeds |
| `||` | Logical OR | First command fails |

---

## Practical Examples

Update packages and install software:

```bash
sudo apt update && sudo apt install nginx
```

Print an error if directory creation fails:

```bash
mkdir test || echo "Could not create directory"
```

Run multiple independent commands:

```bash
date; whoami; pwd
```

---

## Key Takeaways

- `;` runs commands sequentially regardless of result
- `&&` runs the next command only if the previous succeeds
- `||` runs the next command only if the previous fails
- These operators are heavily used in Linux administration and shell scripting
