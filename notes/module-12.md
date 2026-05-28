# Computer Hardware and Linux Basics

## Overview

A computer consists of hardware components that work together to run software and operating systems like Linux. Understanding hardware is essential for installation, configuration, troubleshooting, and system administration.

---

# Motherboard

The **motherboard** (system board) is the main circuit board that connects all hardware components, including:

- CPU
- RAM
- Storage devices
- Expansion cards
- Peripheral devices

Some components are directly attached, while others connect through buses like PCI or USB.

---

# CPU (Central Processing Unit)

The CPU is the brain of the computer where calculations and code execution happen.

## Processor Types

| Type | Description |
|---|---|
| `x86` | 32-bit processor |
| `x86_64` | 64-bit processor |

Advantages of 64-bit systems:

- Supports more RAM
- Better performance
- Improved security

---

# Checking CPU Information

Display CPU architecture:

```bash
arch
```

Detailed CPU information:

```bash
lscpu
```

Example output:

```bash
Architecture: x86_64
CPU op-mode(s): 32-bit, 64-bit
CPU(s): 4
```

---

# RAM and Swap Space

## RAM (Random Access Memory)

RAM temporarily stores running programs and active data.

### Memory Limits

| Architecture | Max RAM |
|---|---|
| 32-bit | ~4 GB |
| 64-bit | Much higher |

---

## Swap Space

Swap is virtual memory stored on disk when RAM is insufficient.

- Inactive RAM data moves to swap
- Helps prevent crashes when memory is low
- Slower than RAM

---

# Checking Memory Usage

```bash
free -m
```

Options:

| Option | Description |
|---|---|
| `-m` | Show MB |
| `-g` | Show GB |

---

# Buses

A **bus** allows communication between computer components.

Common buses:

| Bus | Purpose |
|---|---|
| PCI | Internal expansion devices |
| USB | External devices |

---

# Peripheral Devices

Peripheral devices provide input, output, or storage.

Examples:

- Keyboard
- Mouse
- Monitor
- Printer
- Hard drive

---

# PCI Devices

View PCI-connected hardware:

```bash
lspci
```

Typical devices shown:

- VGA controller
- Network adapter
- Storage controller

---

# USB Devices

USB devices are **hot-plug**, meaning they can be connected while the system is running.

View USB devices:

```bash
lsusb
```

Important:
- Always safely unmount storage devices before removing them.

---

# Storage Devices

Storage devices hold system data and files.

Types include:

- HDD (Hard Disk Drive)
- SSD (Solid State Drive)
- USB drives

---

# Disk Partitioning

A disk can contain multiple partitions.

## Partitioning Types

| Type | Description |
|---|---|
| MBR | Older partitioning system |
| GPT | Modern partitioning system |

Advantages of GPT:

- More partitions
- Supports disks larger than 2 TB

---

# Partition Management Tools

| Tool | Purpose |
|---|---|
| `fdisk` | Manage MBR disks |
| `gdisk` | Manage GPT disks |
| `parted` | Supports both |
| `gparted` | Graphical partition editor |

---

# Linux Device Naming

Storage devices are represented in `/dev`.

Examples:

| Device | Meaning |
|---|---|
| `/dev/sda` | First SATA/SCSI/USB disk |
| `/dev/sda1` | First partition |
| `/dev/sdb` | Second disk |

List storage devices:

```bash
ls /dev/sd*
```

---

# Viewing Partition Information

```bash
fdisk -l /dev/sda
```

Shows:

- Disk size
- Partitions
- Filesystem types

---

# HDD vs SSD

## HDD (Hard Disk Drive)

- Uses spinning disks
- Larger capacity
- Cheaper

## SSD (Solid State Drive)

- No moving parts
- Faster
- Lower power consumption
- More expensive

---

# Optical Drives

Examples:

- CD-ROM
- DVD
- Blu-ray

Mount locations:

| Directory | Purpose |
|---|---|
| `/media` | Modern removable media |
| `/mnt` | Older mount location |

Unmount safely:

```bash
umount
```

---

# Linux Hardware Drivers

Drivers allow Linux to communicate with hardware.

Drivers may be:

- Built into the kernel
- Loaded as modules
- Installed separately

---

# Linux Hardware Compatibility Tips

- Check Linux compatibility before buying hardware
- Avoid very new or specialized devices
- Prefer hardware officially supported by Linux distributions

---

# Video Devices and Displays

Video output requires:

- Video card / GPU
- Monitor

Drivers may be:

- Proprietary
- Open-source

---

# Video Cable Types

| Cable | Description |
|---|---|
| VGA | Analog video |
| DVI | Digital video |
| HDMI | Audio + video, supports 4K |
| DisplayPort | Modern digital interface |

---

# Power Supplies

Power supplies convert AC electricity into DC voltages used by computers.

Common voltages:

- 3.3V
- 5V
- 12V

Good power supplies help protect systems from voltage fluctuations.

---

## Key Linux Hardware Commands

| Command | Purpose |
|---|---|
| `arch` | Show CPU architecture |
| `lscpu` | Detailed CPU info |
| `free -m` | Memory and swap usage |
| `lspci` | PCI devices |
| `lsusb` | USB devices |
| `fdisk -l` | Disk partitions |

---

## What I learned
- The motherboard connects all hardware
- CPUs process instructions and calculations
- RAM stores active data temporarily
- Swap space acts as virtual memory
- PCI and USB buses connect devices
- Linux identifies storage devices under `/dev`
- GPT is newer and more capable than MBR
- SSDs are faster than HDDs
- Drivers are required for hardware support
- Linux supports a wide variety of hardware

---
