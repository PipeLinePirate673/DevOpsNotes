Challenge 1 — Identify Your Network

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
