# How to read `ip neigh`

The general format looks roughly like this:

```text
IP_ADDRESS dev INTERFACE lladdr MAC_ADDRESS STATE
```

For example:

```text
192.168.100.1 dev wlo1 lladdr 14:46:58:45:c8:39 REACHABLE
│              │        │      │                    │
│              │        │      │                    └─ state
│              │        │      └─ MAC address
│              │        └─ Layer 2 address indicator
│              └─ network interface
└─ neighbor's IP address
```

So if you get:

```text
192.168.100.25 dev wlo1 lladdr aa:bb:cc:dd:ee:ff STALE
```

you can extract the following **without any additional knowledge**:

- IP → `192.168.100.25`

- interface → `wlo1`

- MAC → `aa:bb:cc:dd:ee:ff`

- state → `STALE`

---

### How do we know that `fe80::1` is a local network device?

This is where it helps to understand the **context from the previous exercises**.

You have:

```text
fe80::1 dev wlo1
```

`dev wlo1` tells you that this neighbor is reachable through your Wi-Fi interface `wlo1`.

You also have:

```text
router REACHABLE
```

This additionally tells you that Linux identifies this neighbor as a **router** and currently considers the neighbor reachable.

---

---

---







---

---



# ***<mark>TCP VS UDP</mark>***

---



### TCP — Transmission Control Protocol

TCP is **connection-oriented**. It establishes a connection between two devices before sending data.

TCP provides:

- Reliable data delivery

- Data ordering

- Error detection

- Retransmission of lost packets

TCP is useful when **data must arrive correctly and completely**.

Examples:

- SSH → TCP port `22`

- HTTP → TCP port `80`

- HTTPS → TCP port `443`

---

### UDP — User Datagram Protocol

UDP is **connectionless**. It sends data without establishing a connection first.

UDP does not guarantee:

- Data delivery

- Data ordering

- Retransmission of lost packets

UDP has less overhead and can be faster than TCP.

UDP is useful when **speed and low latency are more important than reliability**.

Examples:

- DNS → UDP port `53`

- DHCP → UDP ports `67/68`

### Simple comparison

```text
TCP → Reliable, ordered, connection-oriented
UDP → Fast, lightweight, connectionless
```

A simple way to remember it:

> **TCP:** "Make sure the data arrives correctly."
> 
> **UDP:** "Send the data quickly; don't worry about retransmission."

---

## Listening Port

A **listening port** is a network port on which a program is waiting for incoming connections or traffic.

You can check listening ports with:

```bash
ss -tulpn
```

For example:

```text
tcp   LISTEN   0   128   0.0.0.0:22   0.0.0.0:*   users:(("sshd",pid=1234,fd=3))
```

This means:

- `tcp` → protocol

- `LISTEN` → the program is waiting for incoming connections

- `:22` → listening port

- `sshd` → program using the port

So you can say:

> **SSH is listening on TCP port 22.**

Another example:

```text
udp   UNCONN   0   0   0.0.0.0:53   0.0.0.0:*
```

This means that a program is listening for UDP traffic on port `53`, which is commonly used for DNS.
