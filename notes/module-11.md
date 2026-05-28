# Shell Scripting Basics

## What is a Shell Script?

A shell script is a text file containing executable commands. Scripts automate repetitive tasks and can include logic such as conditions and loops.

Example:

```bash
echo "Hello, World!"
```

Run a script:

```bash
sh test.sh
```

Or make it executable:

```bash
chmod +x test.sh
./test.sh
```

---

# Shebang (`#!`)

Defines which shell interpreter to use.

```bash
#!/bin/bash
```

Common examples:

```bash
#!/bin/sh
#!/bin/bash
```

---

# Using Nano Editor

Open a file:

```bash
nano test.sh
```

Useful shortcuts:

| Shortcut | Description |
|---|---|
| `Ctrl + O` | Save |
| `Ctrl + X` | Exit |
| `Ctrl + K` | Cut line |
| `Ctrl + U` | Paste |
| `Ctrl + W` | Search |
| `Ctrl + G` | Help |

---

# Variables

Assign values:

```bash
ANIMAL="penguin"
```

Access variables using `$`:

```bash
echo "My favorite animal is $ANIMAL"
```

Example:

```bash
#!/bin/bash

ANIMAL="penguin"
echo "My favorite animal is $ANIMAL"
```

---

# Command Substitution

Store command output in variables:

```bash
CURRENT_DIRECTORY=`pwd`
```

Modern syntax:

```bash
CURRENT_DIRECTORY=$(pwd)
```

---

# User Input

Use `read` to get input:

```bash
#!/bin/bash

echo -n "What is your name? "
read NAME

echo "Hello $NAME!"
```

---

# Script Arguments

Arguments are accessed using `$1`, `$2`, etc.

```bash
#!/bin/bash

echo "Hello $1"
```

Run:

```bash
./test.sh World
```

Output:

```bash
Hello World
```

Special variables:

| Variable | Meaning |
|---|---|
| `$0` | Script name |
| `$1-$9` | Arguments |
| `$?` | Previous command exit code |

---

# Exit Codes

| Code | Meaning |
|---|---|
| `0` | Success |
| `>0` | Error |

Example:

```bash
exit 1
```

Check previous exit code:

```bash
echo $?
```

---

# Comments

Anything after `#` is ignored.

```bash
# This is a comment
```

---

# Conditional Statements

Basic syntax:

```bash
if command; then
    # commands
fi
```

Example:

```bash
#!/bin/bash

if grep -q root /etc/passwd; then
    echo "root exists"
else
    echo "root missing"
fi
```

---

# Test Command

Used for comparisons and file checks.

Examples:

```bash
test -f file.txt
test -d /tmp
test 1 -eq 1
test "a" = "a"
```

Common operators:

| Operator | Meaning |
|---|---|
| `-f` | File exists |
| `-d` | Directory exists |
| `-eq` | Equal |
| `-ne` | Not equal |
| `-gt` | Greater than |
| `=` | String equal |
| `!=` | String not equal |

Shortcut syntax:

```bash
if [ -f file.txt ]; then
```

---

# if / elif / else

Example:

```bash
#!/bin/bash

if [ "$1" = "hello" ]; then
    echo "hello yourself"
elif [ "$1" = "goodbye" ]; then
    echo "nice to have met you"
else
    echo "I didn't understand that"
fi
```

---

# case Statements

Cleaner alternative to multiple `if` statements.

```bash
#!/bin/bash

case "$1" in
    hello|hi)
        echo "hello yourself"
        ;;
    goodbye)
        echo "nice to have met you"
        ;;
    *)
        echo "I didn't understand that"
        ;;
esac
```

---

# for Loops

Iterate over a list.

Example:

```bash
#!/bin/bash

SERVERS="servera serverb serverc"

for S in $SERVERS; do
    echo "Doing something to $S"
done
```

Loop through files:

```bash
for FILE in *; do
    echo $FILE
done
```

---

# while Loops

Repeat while a condition is true.

Example:

```bash
#!/bin/bash

i=0

while [ $i -lt 10 ]; do
    echo $i
    i=$(( i + 1 ))
done

echo "Done counting"
```

---

## Key Concepts
- Shell scripts automate tasks
- `#!` defines the interpreter
- Variables use `NAME=value`
- Access variables with `$NAME`
- `read` gets user input
- `$1`, `$2` represent script arguments
- `if`, `case`, `for`, and `while` provide logic control
- Exit code `0` means success
- `test` and `[ ]` are used for comparisons

---
