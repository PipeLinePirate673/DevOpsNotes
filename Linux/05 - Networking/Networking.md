# Linux Networking — Basics

## Introduction

Linux networking is the set of tools and concepts used to configure, inspect, and troubleshoot network connections on a Linux system.

In this section you will learn how to:

- identify network interfaces
- find IP addresses
- understand MAC addresses
- understand IPv4 and IPv6
- inspect routing
- test network connectivity
- understand ports and sockets
- inspect DNS configuration
- troubleshoot common network problems

---

# 1. Network Interfaces

A **network interface** is a network connection provided by the operating system.

Examples:

- `enp2s0` — Ethernet interface
- `eth0` — older/common Ethernet naming
- `wlan0` — older/common Wi-Fi naming
- `wlp3s0` — Wi-Fi interface using modern naming
- `lo` — loopback interface

Display interfaces and addresses:

```bash
ip addr
```

Compact version:

```bash
ip -br addr
```

Display interface state:

```bash
ip link
```

Look for:

- interface name
- `UP` / `DOWN`
- IPv4 address
- IPv6 address
- MAC address

---

# 2. Loopback Interface

The loopback interface is:

```text
lo
```

It is used for communication on the local machine.

The common IPv4 loopback address is:

```text
127.0.0.1
```

Test it:

```bash
ping 127.0.0.1
```

or:

```bash
ping localhost
```

---

# 3. MAC Address

A **MAC address** identifies a network interface at the link layer.

Example:

```text
18:66:da:36:d3:8d
```

Find it with:

```bash
ip link
```

Look for:

```text
link/ether
```

---

# 4. IP Addresses

An IP address identifies a device/interface on an IP network.

Linux commonly uses:

- IPv4
- IPv6

IPv4 example:

```text
192.168.100.19
```

IPv6 example:

```text
fe80::1a66:daff:fe36:d38d
```

---

# 5. Private IPv4 Addresses

Private IPv4 ranges are commonly used inside local networks:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

For example:

```text
192.168.100.19
```

is a private IPv4 address.

---

# 6. Default Gateway

A **default gateway** is the router used when there is no more specific route for the destination.

Display it with:

```bash
ip route
```

Example:

```text
default via 192.168.100.1 dev enp2s0
```

This means:

- `default` → default route
- `via 192.168.100.1` → gateway/router
- `dev enp2s0` → interface used

---

# 7. Routing Table

Linux uses a routing table to decide where network traffic should go.

Display it:

```bash
ip route
```

Example:

```text
default via 192.168.100.1 dev enp2s0
192.168.100.0/24 dev enp2s0 proto kernel scope link src 192.168.100.19
```

---

# 8. Testing Connectivity

`ping` is used to test whether a host can be reached.

Test an IP:

```bash
ping 8.8.8.8
```

Test a hostname:

```bash
ping google.com
```

Stop `ping` with:

```text
Ctrl + C
```

---

# 9. Connectivity Troubleshooting

A useful order is:

Test the local machine:

```bash
ping 127.0.0.1
```

Find the gateway:

```bash
ip route
```

Test the gateway:

```bash
ping <gateway>
```

Test an Internet IP:

```bash
ping 8.8.8.8
```

Test DNS:

```bash
ping google.com
```

This helps identify where the problem occurs.

---

# 10. DNS

**DNS (Domain Name System)** translates domain names into IP addresses.

For example:

```text
google.com → IP address
```

Network connectivity can work even when DNS is broken.

Compare:

```bash
ping 8.8.8.8
```

with:

```bash
ping google.com
```

---

# 11. DNS Tools

Display DNS configuration:

```bash
resolvectl status
```

Query DNS:

```bash
dig google.com
```

Short result:

```bash
dig google.com +short
```

Another DNS tool:

```bash
nslookup google.com
```

---

# 12. Ports

A **port** identifies a network service on a host.

Ports range from:

```text
0–65535
```

Examples:

```text
22   → SSH
80   → HTTP
443  → HTTPS
```

A server application can listen for incoming connections on a specific port.

---

# 13. Listening Ports

Use:

```bash
ss -tulpn
```

Important options:

- `-t` → TCP
- `-u` → UDP
- `-l` → listening
- `-p` → process information
- `-n` → numeric output

Example:

```text
LISTEN 0 128 0.0.0.0:22 0.0.0.0:* users:(("sshd",pid=1234,fd=3))
```

---

# 14. TCP vs UDP

## TCP

TCP is connection-oriented and provides reliable, ordered delivery.

Common examples:

- HTTP/HTTPS
- SSH

## UDP

UDP is connectionless and has lower overhead, but does not guarantee delivery or ordering.

Common examples:

- DNS
- DHCP
- real-time applications

---

# 15. Finding Which Process Uses a Port

Use:

```bash
lsof -i :8080
```

Or:

```bash
ss -tulpn | grep :8080
```

These commands are useful when troubleshooting a service that should be listening on a specific port.

---

# 16. Network Connections

Display TCP and UDP sockets:

```bash
ss -tupn
```

Display all sockets:

```bash
ss -a
```

Useful options:

```text
-t → TCP
-u → UDP
-l → listening
-a → all sockets
-p → process information
-n → numeric output
```

---

# 17. Interface Statistics

Inspect network interface statistics:

```bash
ip -s link
```

You can see information such as:

- received packets
- transmitted packets
- errors
- dropped packets

---

# 18. Quick IP Check

Use:

```bash
ip -br addr
```

Example:

```text
lo       UNKNOWN  127.0.0.1/8
enp2s0   UP       192.168.100.19/24
```

This quickly shows the interface, state, and IP address.

---

# 19. Basic Network Troubleshooting

When a Linux machine cannot connect to something, check step by step.

### Step 1 — Is the interface up?

```bash
ip link
```

Look for:

```text
UP
```

### Step 2 — Does the interface have an IP?

```bash
ip addr
```

### Step 3 — Is there a default route?

```bash
ip route
```

Look for:

```text
default via ...
```

### Step 4 — Can you reach the gateway?

```bash
ping <gateway>
```

### Step 5 — Can you reach an Internet IP?

```bash
ping 8.8.8.8
```

### Step 6 — Does DNS work?

```bash
ping google.com
```

### Step 7 — Is the required service listening?

```bash
ss -tulpn
```

or:

```bash
lsof -i :<PORT>
```

---

# 20. Useful Commands — Quick Reference

| Command             | Purpose                                        |
| ------------------- | ---------------------------------------------- |
| `ip addr`           | Display IP addresses and interfaces            |
| `ip -br addr`       | Display addresses in compact format            |
| `ip link`           | Display interfaces and their state             |
| `ip -s link`        | Display interface statistics                   |
| `ip route`          | Display the routing table                      |
| `ping`              | Test network connectivity                      |
| `ss`                | Display sockets and network connections        |
| `lsof`              | Display open files/resources and network usage |
| `resolvectl status` | Display DNS configuration                      |
| `dig`               | Query DNS                                      |
| `nslookup`          | Query DNS                                      |
| `traceroute`        | Trace the path to a host                       |
| `tracepath`         | Trace the network path to a host               |

---

# Key Concepts to Remember

```text
Network Interface
      ↓
IP Address
      ↓
Routing Table
      ↓
Default Gateway
      ↓
Network / Internet
      ↓
DNS
      ↓
Hostname → IP Address
      ↓
Port
      ↓
Network Service
```

Basic troubleshooting flow:

```text
Interface
    ↓
IP address
    ↓
Route
    ↓
Gateway
    ↓
Internet connectivity
    ↓
DNS
    ↓
Port
    ↓
Service
```

# 
