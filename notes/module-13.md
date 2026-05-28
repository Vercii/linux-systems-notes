# Linux Kernel, Processes, Memory, Logs, and Filesystem Hierarchy

## GNU/Linux Overview

When people say “Linux,” they usually mean **GNU/Linux**:

- **GNU** → User tools and utilities
- **Linux Kernel** → Core of the operating system

The kernel:

- Loads during boot
- Manages hardware resources
- Handles processes and memory
- Provides device access
- Controls networking and filesystems

---

# Linux Kernel Responsibilities

Key kernel functions include:

- Process management
- Memory management
- Device drivers
- Networking
- Virtual filesystems
- System call interface

The shell sends commands to the kernel, which manages hardware and processes.

---

# Pseudo Filesystems

Pseudo filesystems exist in memory, not on disk.

Important pseudo filesystems:

| Directory | Purpose |
|---|---|
| `/proc` | Process and kernel information |
| `/sys` | Hardware and device information |
| `/dev` | Device files |

---

# The `/proc` Directory

Contains information about:

- Running processes
- Kernel configuration
- Hardware
- Memory
- Modules

List contents:

```bash
ls /proc
```

---

# Important `/proc` Files

| File | Description |
|---|---|
| `/proc/cmdline` | Kernel boot parameters |
| `/proc/meminfo` | Memory usage |
| `/proc/modules` | Loaded kernel modules |

---

# Process IDs (PID)

Every running process has a unique PID.

Important notes:

- PID `1` = init/systemd process
- Processes create child processes
- Parent PID is called `PPID`

---

# Process Tree

Display process hierarchy:

```bash
pstree
```

Example:

```text
init
 └─ login
     └─ bash
         └─ pstree
```

---

# Viewing Processes with `ps`

Current shell processes:

```bash
ps
```

Tree view:

```bash
ps --forest
```

All system processes:

```bash
ps aux
```

or

```bash
ps -ef
```

---

# Filtering Processes

Search for a process:

```bash
ps -ef | grep firefox
```

View processes for a user:

```bash
ps -u root
```

---

# The `top` Command

`top` provides real-time process monitoring.

Run:

```bash
top
```

Shows:

- CPU usage
- Memory usage
- Running processes
- System load

Exit:

```text
q
```

---

# Important `top` Actions

| Key | Action |
|---|---|
| `K` | Kill process |
| `R` | Renice process |
| `H` | Help |

---

# Process Priority (Niceness)

Niceness affects scheduling priority.

Range:

```text
-20 (highest priority)
19  (lowest priority)
```

- Lower value = higher priority
- Negative values require root access

---

# Load Average

Shows overall system activity.

Example:

```text
0.12 0.46 0.25
```

Represents system load over:

- 1 minute
- 5 minutes
- 15 minutes

---

# Checking Load Average

```bash
uptime
```

or

```bash
cat /proc/loadavg
```

Interpretation:

- On a 1-core CPU:
  - Load `1.0` = fully utilized
- On a 4-core CPU:
  - Load `1.0` = 25% utilized

---

# Memory Management

Linux uses:

- Physical RAM
- Virtual memory (swap)
- Virtual addressing

Memory is shared efficiently between processes.

---

# Kernel Space vs User Space

| Area | Purpose |
|---|---|
| Kernel Space | Protected kernel memory |
| User Space | Applications and user programs |

Applications communicate with the kernel through system calls.

---

# Viewing Memory Usage

Snapshot:

```bash
free
```

Human-readable:

```bash
free -m
free -g
```

Continuous monitoring:

```bash
free -s 10
```

---

# Understanding `free` Output

| Field | Meaning |
|---|---|
| total | Total memory |
| used | Used memory |
| free | Unused memory |
| buffers/cache | Memory used for caching |
| swap | Virtual memory |

---

# Swap Space

Swap acts as overflow memory stored on disk.

Advantages:
- Prevents crashes from low RAM

Disadvantages:
- Much slower than RAM

---

# Linux Logging

Logs record system and application activity.

Uses:

- Troubleshooting
- Security auditing
- Monitoring system health

---

# Logging Daemons

Common logging systems:

| Daemon | Description |
|---|---|
| `syslogd` | Traditional logging |
| `rsyslogd` | Enhanced syslog |
| `journald` | systemd logging service |

---

# Log File Location

Most logs are stored in:

```text
/var/log
```

---

# Important Log Files

| File | Purpose |
|---|---|
| `boot.log` | Boot messages |
| `cron` | Scheduled task logs |
| `dmesg` | Kernel boot messages |
| `messages` | General system logs |
| `secure` | Authentication logs |
| `journal` | systemd journal logs |
| `Xorg.0.log` | GUI/X server logs |

---

# Viewing Logs

Text logs:

```bash
cat /var/log/messages
less /var/log/messages
```

systemd journal:

```bash
journalctl
```

---

# Log Rotation

Old logs are archived and replaced.

Example:

```text
messages-20261103
```

Prevents logs from filling disk space.

---

# Binary Log Files

Some logs are binary:

| File | Command |
|---|---|
| `/var/log/wtmp` | `last` |
| `/var/log/btmp` | `lastb` |

Check file type:

```bash
file /var/log/wtmp
```

---

# The `dmesg` Command

Displays kernel ring buffer messages.

Useful for:

- Hardware detection
- Driver issues
- USB troubleshooting

Example:

```bash
dmesg | grep -i usb
```

---

# Filesystem Hierarchy Standard (FHS)

FHS defines how Linux directories are organized.

---

# Top-Level Directories

| Directory | Purpose |
|---|---|
| `/` | Root filesystem |
| `/bin` | Essential commands |
| `/boot` | Boot files |
| `/dev` | Device files |
| `/etc` | Configuration files |
| `/home` | User home directories |
| `/lib` | Essential libraries |
| `/media` | Auto-mounted removable media |
| `/mnt` | Temporary mounts |
| `/opt` | Optional third-party software |
| `/proc` | Process/kernel info |
| `/root` | Root user home |
| `/sbin` | System administration commands |
| `/sys` | Hardware information |
| `/tmp` | Temporary files |
| `/usr` | User applications |
| `/var` | Variable data/logs |

---

# `/usr` Hierarchy

Contains:

- User applications
- Shared resources
- Documentation

Examples:

| Directory | Purpose |
|---|---|
| `/usr/bin` | User commands |
| `/usr/lib` | Libraries |
| `/usr/share` | Shared data |
| `/usr/share/doc` | Documentation |

---

# `/usr/local`

Used for software installed manually or compiled from source.

Examples:

```text
/usr/local/bin
/usr/local/lib
```

---

# Binary Directories

## User Commands

```text
/bin
/usr/bin
/usr/local/bin
```

## Administrative Commands

```text
/sbin
/usr/sbin
/usr/local/sbin
```

---

# Library Directories

Shared libraries (`.so` files):

| Directory | Purpose |
|---|---|
| `/lib` | Essential libraries |
| `/lib64` | 64-bit libraries |
| `/usr/lib` | User application libraries |

---

# User Home Directories

Each user gets a home directory:

```text
/home/username
```

Example:

```text
/home/bob
```

---

# Variable Data Directories

The `/var` directory stores changing data.

Examples:

| Directory | Purpose |
|---|---|
| `/var/log` | Log files |
| `/var/cache` | Cache data |
| `/var/spool` | Print/mail queues |
| `/var/tmp` | Persistent temp files |

---

# Important Linux Commands Summary

| Command | Purpose |
|---|---|
| `ps` | View processes |
| `pstree` | Process tree |
| `top` | Real-time monitoring |
| `free` | Memory usage |
| `uptime` | System uptime/load |
| `journalctl` | View systemd logs |
| `dmesg` | Kernel messages |
| `grep` | Filter output |

---

## What I learned
- GNU/Linux combines GNU tools with the Linux kernel
- `/proc` and `/sys` are virtual filesystems
- Every process has a PID
- `ps`, `pstree`, and `top` monitor processes
- Load average reflects CPU usage over time
- Linux separates kernel space and user space
- Logs are mainly stored under `/var/log`
- `dmesg` displays kernel messages
- FHS standardizes Linux directory structure
- `/usr`, `/var`, and `/home` serve different purposes

---
