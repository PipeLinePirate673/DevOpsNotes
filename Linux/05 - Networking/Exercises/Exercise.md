# Linux Networking — Exercises

## Exercise 1 — Network Interfaces

Display all network interfaces. ✅

```bash
ip addr
```

Then use: ✅

```bash
ip link
```

Find:

1. Interface name ✅
   1. `wlo1`
2. IPv4 address ✅
   1. `192.168.100.18`
3. IPv6 address ✅
   1. `fe80::51a2:9770:bb50:3e8`
4. MAC address ✅
   1. `08:8e:90:b2:45:71`
5. Interface state (`UP` / `DOWN`) ✅
   1. `UP`

---

## Exercise 2 — Compact Interface Overview

Display network interfaces in a compact format.

```bash
ip -br addr
```

Identify:

1. All interfaces   ✅
   1. `lo` `wlo1` `docker0`
2. Which interface is used for Ethernet ✅
   1. `There is no Ethernet on my laptop so I don't see Ethernet interface`
3. Which interface is used for Wi-Fi ✅
   1. `wlo1`
4. Which interface is the loopback interface ✅
   1. `lo`
5. IPv4 address of the active network interface ✅
   1. `192.168.100.18`

---

## Exercise 3 — MAC Address

Find the MAC address of your active network interface.

```bash
ip link
```

Find:

```text
link/ether
```

Answer:

1. What is the interface name? ✅
   1. `wlo1`
2. What is its MAC address? ✅
   1. ` 08:8e:90:b2:45:71`
3. Is the interface `UP` or `DOWN`? ✅
   1. `UP`

---

## Exercise 4 — Loopback

Investigate the loopback interface.

```bash
ip addr show lo
```

Then test it:

```bash
ping -c 4 127.0.0.1
```

Find:

1. Interface name ✅
   
   1. `lo`

2. IPv4 address ✅
   
   1. `127.0.0.1/8`

3. Interface state ✅
   
   1. `UNKNOW`

4. Whether the ping succeeds ✅
   
   1. ```bash
      dominik@Zenbook:~$ ping -c 4 127.0.0.1
      PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
      64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.050 ms
      64 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.087 ms
      64 bytes from 127.0.0.1: icmp_seq=3 ttl=64 time=0.105 ms
      64 bytes from 127.0.0.1: icmp_seq=4 ttl=64 time=0.105 ms
      
      --- 127.0.0.1 ping statistics ---
      4 packets transmitted, 4 received, 0% packet loss, time 3062ms
      rtt min/avg/max/mdev = 0.050/0.086/0.105/0.022 ms
      ```

---

## Exercise 5 — IP Address

Find the IPv4 address currently assigned to your active network interface.

```bash
ip -4 addr
```

Answer:

1. Interface name ✅
   
   1. `wlo1`

2. IPv4 address ✅
   
   1. `192.168.100.18/24`

3. Network prefix✅
   
   1. `/24`
   
   ---

## Exercise 6 — Routing Table

Display the routing table.

```bash
ip route
```

Find:

1. Default route ✅
   1. `default via 192.168.100.1 dev wlo1 proto dhcp src 192.168.100.18 metric 600 `
2. Default gateway ✅
   1. `192.168.100.1`
3. Interface used for the default route ✅
   1. `dev wlo1`
4. Source IP address ✅
   1. `192.168.100.18`

---

## Exercise 7 — Route Investigation

Find out which route Linux would use to reach `8.8.8.8`.

```bash
ip route get 8.8.8.8
```

Identify:

1. Gateway ✅
   1. `192.168.100.1`
2. Network interface ✅
   1. `dev wlo1`
3. Source IP ✅
   1. `192.168.100.18`
4. Destination IP ✅
   1. `8.8.8.8`

---

## Exercise 8 — Neighbor Table

Display the neighbor table.

```bash
ip neigh
```

Find:

1. At least one local network device
2. Its IP address
3. Its MAC address
4. Its state

---

## Exercise 9 — Connectivity

Test connectivity to the following:

### Local machine

```bash
ping -c 4 127.0.0.1
```

### Default gateway

First find the gateway:

```bash
ip route
```

Then:

```bash
ping -c 4 <GATEWAY>
```

### Internet IP

```bash
ping -c 4 8.8.8.8
```

### Domain name

```bash
ping -c 4 google.com
```

Record:

- Does each test succeed?
- What does each test tell you?

---

## Exercise 10 — DNS

Check your DNS configuration.

```bash
resolvectl status
```

Then resolve a domain:

```bash
dig google.com +short
```

Find:

1. DNS server
2. Resolved IP address
3. Network interface used by the DNS configuration

---

## Exercise 11 — DNS Investigation

Compare:

```bash
ping -c 4 8.8.8.8
```

and:

```bash
ping -c 4 google.com
```

Answer:

1. Does the IP address work?
2. Does the domain name work?
3. What would it mean if the IP worked but the domain did not?

---

## Exercise 12 — Listening Ports

Display listening TCP and UDP sockets.

```bash
ss -tulpn
```

Find:

1. One TCP listening port
2. One UDP listening port, if available
3. Process name
4. PID
5. Local address
6. Port number

---

## Exercise 13 — Active Connections

Display active TCP and UDP connections.

```bash
ss -tupn
```

Choose one `ESTAB` connection.

Find:

1. Protocol
2. State
3. Local IP
4. Local port
5. Remote IP
6. Remote port
7. Process name
8. PID

Explain which port is local and which port is remote.

---

## Exercise 14 — Listening vs Established

Run:

```bash
ss -tulpn
```

Then:

```bash
ss -tupn
```

Compare the results.

Answer:

1. What does `LISTEN` mean?
2. What does `ESTAB` mean?
3. Why can an `ESTAB` connection appear in `ss -tupn` but not in `ss -tulpn`?
4. What is the difference between a listening port and a local ephemeral port?

---

## Exercise 15 — Find a Process Using a Port

Choose a port that is currently in use.

```bash
lsof -i :<PORT>
```

Find:

1. Process name
2. PID
3. User
4. Protocol
5. Local address
6. Local port
7. Remote address
8. Remote port

---

## Exercise 16 — Find Port 8080

Check whether anything is using port `8080`.

```bash
lsof -i :8080
```

Also check:

```bash
ss -tulpn | grep :8080
```

Answer:

1. Is anything listening on port `8080`?
2. If yes, what is the process?
3. What is its PID?
4. If nothing is using the port, explain what that means.

---

## Exercise 17 — Network Interface Statistics

Display interface statistics.

```bash
ip -s link
```

Choose one active interface.

Find:

1. RX packets
2. RX errors
3. RX dropped packets
4. TX packets
5. TX errors
6. TX dropped packets

---

## Exercise 18 — NetworkManager

Check NetworkManager devices.

```bash
nmcli device status
```

Find:

1. Device name
2. Device type
3. Connection state
4. Connection name

Then run:

```bash
nmcli connection show
```

Identify the active connection.

---

# Exercise 19 — Network Troubleshooting Scenario

Imagine your Linux machine cannot access the Internet.

Investigate the problem using standard Linux tools.

Start with:

```bash
ip link
```

Then:

```bash
ip addr
```

Then:

```bash
ip route
```

Then test:

```bash
ping -c 4 <GATEWAY>
```

```bash
ping -c 4 8.8.8.8
```

```bash
ping -c 4 google.com
```

Finally check:

```bash
resolvectl status
```

Determine:

1. Is the interface up?
2. Does it have an IP address?
3. Is there a default gateway?
4. Can the machine reach the gateway?
5. Can it reach the Internet by IP?
6. Does DNS work?
7. Where is the problem?

---

# Exercise 20 — Network Service Investigation

Imagine a web application should be available on port `8080`.

Investigate it without using a GUI.

Use:

```bash
ss -tulpn
```

and:

```bash
lsof -i :8080
```

Find:

1. Is port `8080` listening?
2. Which process is using it?
3. What is its PID?
4. What protocol is being used?
5. What local address is it listening on?
6. What does `0.0.0.0:8080` mean?
7. What does `127.0.0.1:8080` mean?

---

# Challenge 1 — Identify Your Network

Without looking at previous exercises, find:

1. Active network interface
2. Interface type
3. MAC address
4. IPv4 address
5. IPv6 address
6. Default gateway
7. Default route
8. DNS server

Useful commands:

```bash
ip -br addr
ip link
ip route
resolvectl status
```

---

# Challenge 2 — Investigate an Active Connection

Run:

```bash
ss -tupn
```

Choose one active `ESTAB` connection.

Investigate:

1. Process name
2. PID
3. Protocol
4. Local IP
5. Local port
6. Remote IP
7. Remote port
8. Connection state

Then explain:

> Why is the local port different from the remote port?

---

# Challenge 3 — Port Investigation

Choose any active connection from:

```bash
ss -tupn
```

Then investigate its process.

Use:

```bash
ps -fp <PID>
```

and:

```bash
lsof -p <PID>
```

Find:

1. Process name
2. PID
3. User
4. Parent PID
5. CPU usage
6. Memory usage
7. Command
8. Open files
9. Network connections

---

# Final Challenge — Network Investigation

Without looking at your notes, answer these questions:

1. What is a network interface?
2. What is a MAC address?
3. What is an IP address?
4. What is the difference between IPv4 and IPv6?
5. What is `127.0.0.1`?
6. What is the loopback interface?
7. What is a default gateway?
8. What is a routing table?
9. What does `ip route` show?
10. What does `ping` test?
11. What is DNS?
12. What does `dig` do?
13. What is a port?
14. What is the difference between TCP and UDP?
15. What does `ss` show?
16. What does `LISTEN` mean?
17. What does `ESTAB` mean?
18. What does `lsof -i :8080` do?
19. What is an ephemeral port?
20. How would you troubleshoot a Linux machine that cannot access the Internet?

---

# Goal

Build the ability to investigate Linux networking using standard command-line tools.

You should be able to:

```text
Interface
    ↓
IP address
    ↓
MAC address
    ↓
Routing
    ↓
Gateway
    ↓
Connectivity
    ↓
DNS
    ↓
Ports
    ↓
Sockets
    ↓
Processes
    ↓
Troubleshooting
```
