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

### One important thing

Your earlier entry:

```text
192.168.100.1 dev wlo1 lladdr 14:46:58:45:c8:39 REACHABLE
```

**didn't come out of nowhere**. It was probably an entry that you had in the neighbor table a moment earlier. The entry can disappear or change because the neighbor table is dynamic.

If you want to see your **gateway** `192.168.100.1` in `ip neigh`, run:

```bash
ping -c 1 192.168.100.1
ip neigh
```

Linux will then need to resolve the gateway's MAC address using ARP, and you should see something like:

```text
192.168.100.1 dev wlo1 lladdr 14:46:58:45:c8:39 REACHABLE
```

You can then use this entry to complete Exercise 8.

**The most important rule:** when doing exercises like these, first look at the **format of the output**, and then identify the information you need. You don't have to memorize where every piece of information is located.
