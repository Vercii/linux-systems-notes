# Linux User Accounts, Groups, and Administrative Access

## Overview

User accounts are designed to provide security on a Linux operating system. Each person on the system must log in using a user account which either allows the person to access specific files and directories or disallows such access, accomplished using file permissions, which are file and directory permissions given by the system to users, groups and everyone else who logs in. These permissions can be edited by the root user.

User accounts also belong to groups, which can also be used to provide access to files/directories. Each user belongs to at least one group (often many) to allow users to more easily share data that is stored in files with other users.

User and group account data is stored in database files. Knowing the content of these files allows you to better understand which users have access to files and directories on the system. These database files also contain vital security information that may affect the ability of a user to log in and access the system.

Several commands provide the ability to see user and group account information, as well as to switch from one user account to another (provided you have the appropriate authority to do so). These commands are valuable for investigating usage of the system, troubleshooting system problems and for monitoring unauthorized access to the system.

---

# Root Access and Administrative Privileges

There are many different ways to execute a command that requires administrative or root privileges. Logging in to the system as the root user allows you to execute commands as the administrator. This access is potentially dangerous because you may forget that you are logged in as root and might run a command that could cause problems on the system. As a result, it is not recommended to log in as the root user directly.

Because using the root account is potentially dangerous, you should only execute commands as root if administrative privileges are needed. If the root account is disabled, as it is on the Ubuntu distribution, then administrative commands can be executed using the `sudo` command. If the root account is enabled, then a regular user can execute the `su` command to switch accounts to the root account.

When you log in to the system directly as root to execute commands, then everything about your session runs as the root user. If using the graphical environment, this is especially dangerous as the graphical login process is comprised of many different executables (programs that run during login). Each program that runs as the root user represents a greater threat than a process run as a standard user, as those programs would be allowed to do nearly anything, whereas standard user programs are very restricted in what they can do.

The other potential danger with logging into the system as root is that a person that does this may forget to log out to do their non-administrative work, allowing programs such as browsers and email clients to be run as the root user without restrictions on what they could do.

The fact that several distributions of Linux, notably Ubuntu, do not allow users to log in as the root user should be enough indication that this is not the preferred way to perform administrative tasks.

---

# The `su` Command

The `su` command allows you to run a shell as a different user. While switching to the root user is what the `su` command is used for most frequently, it can also switch to other users as well.

## Syntax

```bash
su [options] [username]
```

When switching users, utilizing the login shell option is recommended, as the login shell fully configures the new shell with the settings of the new user, ensuring any commands executed run correctly.

If this option is omitted, the new shell changes the UID but doesn't fully log in the user.

## Login Shell Options

```bash
su -
su -l
su --login
```

By default, if a username is not specified, the `su` command opens a new shell as the root user.

The following two commands are equivalent ways to start a shell as the root user:

```bash
su - root
su -
```

After pressing Enter to execute either one of these commands, the user must provide the password of the root user to start the new shell. If you don't know the password of the account that you are shifting to, then the `su` command will fail.

## Example

```bash
sysadmin@localhost:~$ su -
Password: netlab123
root@localhost:~# id
uid=0(root) gid=0(root) groups=0(root)
```

After using the shell started by the `su` command to perform the necessary administrative tasks, return to your original shell (and original user account) by using the `exit` command.

```bash
root@localhost:~# exit
logout
sysadmin@localhost:~$ id
uid=1001(sysadmin) gid=1001(sysadmin) groups=1001(sysadmin),4(adm),27(sudo)
```

---

# The `sudo` Command

The `sudo` command allows users to execute commands as another user. Similar to the `su` command, the root user is assumed by default.

## Syntax

```bash
sudo [options] command
```

In distributions that do not allow the root user to login directly or via the `su` command, the installation process automatically configures one user account to be able to use the `sudo` command to execute commands as if the root user executed them.

For example, administrative privileges are necessary to view the `/etc/shadow` file:

```bash
sysadmin@localhost:~$ head /etc/shadow
head: cannot open '/etc/shadow' for reading: Permission denied
```

When using the `sudo` command to execute a command as the root user, the command prompts for the user's own password, not that of the root user.

The prompt for the password will not appear again as long as the user continues to execute `sudo` commands less than five minutes apart.

## Example

```bash
sysadmin@localhost:~$ sudo head /etc/shadow
[sudo] password for sysadmin: netlab123
root:$6$4Yga95H9$8HbxqsMEIBTZ0YomlMffYCV9VE1SQ4T2H3SHXw41M02SQtfAdDVE9mqGp2hr20q.ZuncJpLyWkYwQdKlSJyS8.:16464:0:99999:7:::
daemon:*:16463:0:99999:7:::
bin:*:16463:0:99999:7:::
sys:*:16463:0:99999:7:::
sync:*:16463:0:99999:7:::
games:*:16463:0:99999:7:::
man:*:16463:0:99999:7:::
lp:*:16463:0:99999:7:::
mail:*:16463:0:99999:7:::
news:*:16463:0:99999:7:::
```

## Advantages of `sudo`

* Uses the current user's password instead of the root password
* Reduces the need to share the root password
* Logs all administrative commands
* Reduces accidental execution of commands as root
* Improves accountability and auditing

---

# User Account Information

There are several text files in the `/etc` directory that contain the account data of the users and groups defined on the system.

For example, to see if a specific user account has been defined on the system, check the `/etc/passwd` file.

---

# The `/etc/passwd` File

The `/etc/passwd` file defines some of the account information for user accounts.

## Example

```bash
sysadmin@localhost:~$ tail -5 /etc/passwd
syslog:x:101:103::/home/syslog:/bin/false
bind:x:102:105::/var/cache/bind:/bin/false
sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin
operator:x:1000:37::/root:/bin/sh
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

Each line contains information pertaining to a single user. The data is separated into fields by colon characters.

## `/etc/passwd` Fields

### 1. Username

```text
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

The first field contains the name of the user or the username.

---

### 2. Password Placeholder

```text
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

The `x` indicates that the encrypted password is stored in the `/etc/shadow` file.

---

### 3. User ID (UID)

```text
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

Each account is assigned a user ID (UID).

---

### 4. Primary Group ID (GID)

```text
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

Indicates the user's primary group.

---

### 5. Comment Field

```text
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

Can contain additional user information.

---

### 6. Home Directory

```text
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

Defines the location of the user's home directory.

Examples:

```text
/home/sysadmin
/root
```

---

### 7. Login Shell

```text
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

Defines the user's default shell.

Common shell:

```text
/bin/bash
```

---

# Searching for User Accounts

## Using `grep`

```bash
sysadmin@localhost:~$ grep sysadmin /etc/passwd
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

---

# The `/etc/shadow` File

The `/etc/shadow` file contains account information related to user passwords.

Regular users cannot view this file for security reasons.

## Switching to Root

```bash
sysadmin@localhost:~$ su -
Password: netlab123
root@localhost:~#
```

## Example `/etc/shadow` Output

```bash
root@localhost:~# tail -5 /etc/shadow
syslog:*:16874:0:99999:7:::
bind:*:16874:0:99999:7:::
sshd:*:16874:0:99999:7:::
operator:!:16874:0:99999:7:::
sysadmin:$6$c75ekQWF$.GpiZpFnIXLzkALjDpZXmjxZcIll14OvL2mFSIfnc1aU2cQ/221QL5AX5RjKXpXPJRQ0uVN35TY3/..c7v0.n0:16874:5:30:7:60:15050:
```

---

# `/etc/shadow` Fields

## 1. Username

Contains the username matching `/etc/passwd`.

---

## 2. Password

Contains the encrypted password hash.

System accounts often use:

```text
*
```

---

## 3. Last Change

Represents the last password change date in days since January 1, 1970 (Epoch).

---

## 4. Minimum

Minimum number of days before a password can be changed again.

Example:

```text
5
```

Means the password cannot be changed again for 5 days.

---

## 5. Maximum

Maximum number of days the password remains valid.

Example:

```text
30
```

Means the password must be changed every 30 days.

```text
99999
```

Effectively means no expiration.

---

## 6. Warn

Number of days before password expiration that users receive warnings.

Example:

```text
7
```

---

## 7. Inactive

Grace period after password expiration before the account is locked.

Example:

```text
60
```

---

## 8. Expire

Defines the date when the account expires.

Used commonly for temporary employees or contractors.

---

## 9. Reserved

Currently unused.

---

# The `getent` Command

The `getent` command retrieves entries from databases such as `/etc/passwd` and `/etc/shadow`.

## Syntax

```bash
getent database record
```

## Example

```bash
sysadmin@localhost:~$ getent passwd sysadmin
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

One advantage of `getent` is that it can retrieve account information from both local files and network directory servers.

---

# User Types

## Regular Users

* Typically have UID values greater than 500 or 1000
* Used for normal logins

## Root User

* UID = 0
* Has unrestricted administrative privileges

## System Accounts

* Usually UID 1–499
* Used for services and daemons
* Not intended for interactive login

### Example

```text
sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin
```

In `/etc/shadow`:

```text
sshd:*:16874:0:99999:7:::
```

---

# Groups and Group Membership

A user's access is also determined by group memberships.

The `/etc/passwd` file defines the primary group membership.

Supplemental groups are stored in `/etc/group`.

---

# The `/etc/group` File

The `/etc/group` file is colon-delimited.

## Example

```text
mail:x:12:mail,postfix
```

## Fields

### 1. Group Name

```text
mail
```

---

### 2. Password Placeholder

```text
x
```

Actual group passwords are stored in `/etc/gshadow`.

---

### 3. Group ID (GID)

```text
12
```

---

### 4. User List

```text
mail,postfix
```

Lists secondary group members.

---

# Viewing Group Information

## Using `grep`

```bash
sysadmin@localhost:~$ grep mail /etc/group
mail:x:12:mail,postfix
```

## Using `getent`

```bash
sysadmin@localhost:~$ getent group mail
mail:x:12:mail,postfix
```

---

# The `id` Command

The `id` command displays user and group information.

## Syntax

```bash
id [options] username
```

## Current User Example

```bash
sysadmin@localhost:~$ id
uid=1001(sysadmin) gid=1001(sysadmin) groups=1001(sysadmin),4(adm),27(sudo)
```

## Specific User Example

```bash
sysadmin@localhost:~$ id root
uid=0(root) gid=0(root) groups=0(root)
```

## Show Primary Group

```bash
sysadmin@localhost:~$ id -g
1001
```

## Show All Groups

```bash
sysadmin@localhost:~$ id -G
1001 4 27
```

## Verifying Groups

```bash
sysadmin@localhost:~$ cat /etc/group | grep sysadmin
adm:x:4:syslog,sysadmin
sudo:x:27:sysadmin
sysadmin:x:1001:
```

---

# The `who` Command

The `who` command displays currently logged-in users.

## Example

```bash
sysadmin@localhost:~$ who
root       tty2        2013-10-11 10:00
sysadmin   tty1        2013-10-11 09:58 (:0)
sysadmin   pts/0       2013-10-11 09:59 (:0.0)
sysadmin   pts/1       2013-10-11 10:00 (example.com)
```

## Output Fields

| Field    | Description      |
| -------- | ---------------- |
| Username | Logged-in user   |
| Terminal | Terminal session |
| Date     | Login time       |
| Host     | Login source     |

### Terminal Types

* `tty` → local terminal
* `pts` → pseudo terminal or remote session

---

# Additional `who` Options

## Show Last Boot Time and Runlevel

```bash
sysadmin@localhost:~$ who -b -r
         system boot    2013-10-11 09:54
         run-level 5    2013-10-11 09:54
```

---

# The `w` Command

The `w` command provides detailed information about logged-in users and system status.

## Example

```bash
sysadmin@localhost:~$ w
 10:44:03 up 50 min,  4 users,  load average: 0.78, 0.44, 0.19
USER       TTY     FROM         LOGIN@   IDLE   JCPU   PCPU   WHAT
root       tty2    -            10:00    43:44  0.01s  0.01s  -bash
sysadmin   tty1    :0           09:58    50:02  5.68s  0.16s  pam: gdm-password
sysadmin   pts/0   :0.0         09:59    0.00s  0.14s  0.13s  ssh 192.168.1.2
sysadmin   pts/1   example.com  10:00    0.00s  0.03s  0.01s  w
```

## First Line Meaning

```text
10:44:03 up 50 min, 4 users, load average: 0.78, 0.44, 0.19
```

Displays:

* Current time
* System uptime
* Number of logged-in users
* CPU load averages for:

  * 1 minute
  * 5 minutes
  * 15 minutes

---

# `w` Command Columns

| Column | Description              |
| ------ | ------------------------ |
| USER   | Logged-in username       |
| TTY    | Terminal                 |
| FROM   | Login source             |
| LOGIN@ | Login time               |
| IDLE   | Idle time                |
| JCPU   | Total CPU time           |
| PCPU   | Current process CPU time |
| WHAT   | Current command/process  |

> Note: `s` means seconds.

---

# The `last` Command

The `last` command displays login history.

It reads from:

```text
/var/log/wtmp
```

## Example

```bash
sysadmin@localhost:~$ last
sysadmin console Tue Sep 18 02:31   still logged in
sysadmin console                    Tue Sep 18 02:31 - 02:31  (00:00)
wtmp begins Tue Sep 18 02:31:57 2018
```

Unlike `who` and `w`, the `last` command shows both current and previous login sessions.

If the user is still logged in, it displays:

```text
still logged in
```

Otherwise, it shows the session duration.

---

# Important Log Files

| File            | Purpose                                |
| --------------- | -------------------------------------- |
| `/etc/passwd`   | User account information               |
| `/etc/shadow`   | Encrypted passwords and password aging |
| `/etc/group`    | Group definitions                      |
| `/etc/gshadow`  | Group passwords                        |
| `/var/log/utmp` | Current logged-in users                |
| `/var/log/wtmp` | Login history                          |

---

# Summary

Linux user and group management is fundamental to system security and administration. Key concepts include:

* User accounts and permissions
* Groups and access control
* Root privileges and administrative safety
* Important account database files
* Commands for managing and viewing users
* Monitoring logged-in users and login history

Essential commands covered:

```bash
su
sudo
id
who
w
last
grep
getent
```

Essential files covered:

```text
/etc/passwd
/etc/shadow
/etc/group
/etc/gshadow
/var/log/utmp
/var/log/wtmp
```
