# Networking Fundamentals and Linux Networking Commands

Before setting up a network or accessing an existing network, it is beneficial to know some key networking terms and Linux networking concepts. This document summarizes the most important terms, protocols, configuration files, and commands used in Linux networking.

---

# Basic Networking Terms

## Host
A **host** is any device that communicates on a network.

Examples:
- Desktop computers
- Laptops
- Smartphones
- Servers
- Smart TVs

---

## Network
A **network** is a collection of two or more hosts that can communicate with each other.

Connections may be:
- Wired
- Wireless

---

## Internet
The **Internet** is a massive public network connecting millions of hosts worldwide.

Common uses:
- Browsing websites
- Email
- Streaming
- Cloud services

---

## Wi-Fi
**Wi-Fi** refers to wireless networking technology.

---

## Server
A **server** is a host that provides services to other hosts.

Examples:
- Web server
- Mail server
- File server

---

## Service
A **service** is a feature or functionality provided by a host.

Example:
- A web server provides web pages.

---

## Client
A **client** is a host that accesses services from a server.

Example:
- Your laptop accessing a website.

---

## Router / Gateway
A **router** (or gateway) connects different networks together.

Example:
- A home router connects your local network to the Internet.

---

# Additional Networking Terms

## Packet
A **packet** is a small chunk of data sent across a network.

Breaking communication into packets improves efficiency.

---

## IP Address
An **IP address** uniquely identifies a host on a network.

### IPv4 Example
```bash
192.168.1.2
```

### IPv6 Example
```bash
2001:0db8:85a3:0042:1000:8a2e:0370:7334
```

---

## Mask / Netmask / Subnet Mask
A **subnet mask** defines which IP addresses belong to the same network.

Example:
```bash
255.255.255.0
```

---

## Hostname
A **hostname** is a human-readable name assigned to a host.

Examples:
```bash
server1
google.com
```

---

## URL
A **Uniform Resource Locator (URL)** is a web address.

Example:
```bash
https://www.example.com
```

---

## DHCP
**Dynamic Host Configuration Protocol (DHCP)** automatically assigns:
- IP addresses
- DNS servers
- Gateways
- Subnet masks

---

## DNS
**Domain Name System (DNS)** translates hostnames into IP addresses.

Example:
```text
google.com → 142.250.190.14
```

---

## Ethernet
**Ethernet** is the most common wired networking technology.

Common speeds:
- 10 Mbps
- 100 Mbps
- 1 Gbps
- 100 Gbps

---

## TCP/IP
**Transmission Control Protocol/Internet Protocol (TCP/IP)** is the standard protocol suite used for Internet communication.

---

# IPv4 and IPv6

## IPv4
IPv4 uses 32-bit addresses.

Example:
```bash
192.168.1.2
```

Maximum possible addresses:
- Approximately 4.3 billion

### Problem
IPv4 addresses began running out.

---

## IPv6
IPv6 uses 128-bit addresses.

Example:
```bash
2001:db8::1
```

Advantages:
- Massive address space
- Improved efficiency
- Better routing
- Improved packet handling

---

# NAT (Network Address Translation)

NAT allows multiple devices to share a single public IP address.

Example:
```text
10 local devices → 1 public IP
```

This delayed the urgent migration from IPv4 to IPv6.

---

# DHCP vs Static IP Addressing

## DHCP
Automatic configuration.

Commonly used for:
- Laptops
- Smartphones
- Wireless devices

---

## Static IP
Manual configuration.

Commonly used for:
- Servers
- Routers
- Infrastructure devices

---

# Linux Network Configuration Files

# `/etc/hosts`

Local hostname-to-IP mappings.

Example:
```bash
127.0.0.1 localhost
```

---

# `/etc/resolv.conf`

DNS server configuration.

Example:
```bash
nameserver 8.8.8.8
```

Multiple nameservers can be specified:
```bash
nameserver 8.8.8.8
nameserver 1.1.1.1
```

---

# `/etc/nsswitch.conf`

Controls the order of hostname resolution.

Example:
```bash
hosts: files dns
```

Meaning:
1. Check `/etc/hosts`
2. Then check DNS

Alternative:
```bash
hosts: dns files
```

Meaning:
1. Check DNS first
2. Then check `/etc/hosts`

---

# CentOS Network Interface Configuration

## IPv4 Configuration File

```bash
/etc/sysconfig/network-scripts/ifcfg-eth0
```

Example static configuration:
```bash
DEVICE="eth0"
BOOTPROTO=none
ONBOOT=yes
TYPE="Ethernet"
IPADDR=192.168.1.1
PREFIX=24
GATEWAY=192.168.1.1
DNS1=192.168.1.2
```

### DHCP Configuration
```bash
BOOTPROTO=dhcp
```

---

# IPv6 Configuration

Add the following to the same interface configuration file:

```bash
IPV6INIT=yes
IPV6ADDR=<IPv6 Address>
IPV6_DEFAULTGW=<Gateway Address>
```

For DHCPv6:
```bash
DHCPV6C=yes
```

Enable IPv6 networking:
```bash
NETWORKING_IPV6=yes
```

---

# Restarting Network Interfaces

## Restart One Interface

```bash
ifdown eth0
ifup eth0
```

---

## Restart Entire Networking Service

```bash
service network restart
```

This restarts all interfaces.

---

# Network Commands

# `ifconfig`

Displays network interface configuration.

Example:
```bash
ifconfig
```

Shows:
- IP addresses
- MAC addresses
- Interface status
- RX/TX statistics

Deprecated on many systems.

---

# `ip`

Modern replacement for:
- ifconfig
- route
- arp

---

## Show Interfaces

```bash
ip addr show
```

---

## Show Routes

```bash
ip route show
```

---

# `route`

Displays the routing table.

Example:
```bash
route
```

Numeric output:
```bash
route -n
```

Deprecated in favor of:
```bash
ip route
```

---

# Routing Table Example

```bash
Destination     Gateway         Genmask         Iface
192.168.1.0     0.0.0.0         255.255.255.0   eth0
0.0.0.0         192.168.1.1     0.0.0.0         eth0
```

Meaning:
- Local traffic stays local
- All other traffic goes to the router

---

# `ping`

Tests network connectivity.

Example:
```bash
ping -c 4 google.com
```

Successful ping:
```text
4 packets transmitted, 4 received
```

Failed ping:
```text
Destination Host Unreachable
```

---

# `netstat`

Displays:
- Connections
- Routing tables
- Ports
- Interface statistics

---

## Show Interface Statistics

```bash
netstat -i
```

Important fields:
- TX-OK
- TX-ERR

---

## Show Routing Table

```bash
netstat -r
```

---

## Show Open Listening Ports

```bash
netstat -tln
```

Options:
- `-t` → TCP
- `-l` → Listening
- `-n` → Numeric output

---

# Ports

A **port** identifies a specific network service.

Example:
- SSH uses port 22

If port 22 is listening:
```text
0.0.0.0:22 LISTEN
```

SSH is available remotely.

---

# `ss`

Modern replacement for netstat.

Displays:
- Socket statistics
- Connections
- Listening ports

---

## Show Connections

```bash
ss
```

---

## Show Statistics

```bash
ss -s
```

---

# DNS Troubleshooting

# `dig`

Performs DNS queries.

Example:
```bash
dig example.com
```

Shows:
- DNS answers
- Query time
- DNS server used

---

# `host`

Simple DNS lookup utility.

---

## Hostname to IP

```bash
host google.com
```

---

## IP to Hostname

```bash
host 8.8.8.8
```

---

## Query CNAME Records

```bash
host -t CNAME example.com
```

---

## Query SOA Records

```bash
host -t SOA example.com
```

---

## Show All DNS Information

```bash
host -a example.com
```

---

# SSH

Secure Shell (SSH) allows remote login to another machine.

---

## Connect to Remote Machine

```bash
ssh username@hostname
```

Example:
```bash
ssh bob@test
```

---

## Exit SSH Session

```bash
exit
```

---

# Loopback Interface

The loopback device:
```bash
lo
```

IP address:
```bash
127.0.0.1
```

Purpose:
- Allows the system to communicate with itself.

---

# Important Networking Concepts

## Name Resolution Process

1. Check `/etc/nsswitch.conf`
2. Check `/etc/hosts`
3. Check DNS servers in `/etc/resolv.conf`

---

# DNS Keywords

## `domain`

Automatically appends a domain name.

Example:
```bash
domain example.com
```

Typing:
```bash
server1
```

May become:
```bash
server1.example.com
```

---

## `search`

Searches multiple domains.

Example:
```bash
search example.com company.local
```

---

# Common Linux Networking Commands Cheat Sheet

## Interface Information
```bash
ifconfig
ip addr show
```

---

## Routing Information
```bash
route -n
ip route show
```

---

## Connectivity Testing
```bash
ping google.com
```

---

## DNS Queries
```bash
dig google.com
host google.com
```

---

## Open Ports
```bash
netstat -tln
ss -tln
```

---

## SSH Remote Login
```bash
ssh user@host
```

---

## Remember
- IPv4 uses 32-bit addresses
- IPv6 uses 128-bit addresses
- DNS translates names to IP addresses
- DHCP automatically assigns network settings
- Routers connect networks
- NAT allows multiple devices to share one IP
- Ports identify services
- SSH provides secure remote access
- `ip` replaces `ifconfig`
- `ss` replaces `netstat`

---

# Simple Networking Flow

```text
Host
  ↓
IP Address
  ↓
Packets
  ↓
Switch / Wi-Fi
  ↓
Router / Gateway
  ↓
Internet
  ↓
DNS resolves names
  ↓
Server responds
```
