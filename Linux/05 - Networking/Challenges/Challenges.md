# Challenge 1 — Identify Your Network

Without looking at previous exercises, find:



```bash
dominik@Zenbook:~/Pulpit/DevOpsNotes/DevOps Notes$ ip -br addr
lo               UNKNOWN        127.0.0.1/8 ::1/128 
wlo1             UP             192.168.100.18/24 fe80::51a2:9770:bb50:3e8/64 
docker0          DOWN           172.17.0.1/16
```

```bash
dominik@Zenbook:~/Pulpit/DevOpsNotes/DevOps Notes$ ip link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: wlo1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DORMANT group default qlen 1000
    link/ether 08:8e:90:b2:45:71 brd ff:ff:ff:ff:ff:ff
    altname wlp0s20f3
    altname wlx088e90b24571
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default 
    link/ether ee:48:e1:91:a2:32 brd ff:ff:ff:ff:ff:ff

```

```bash
dominik@Zenbook:~/Pulpit/DevOpsNotes/DevOps Notes$ ip route
default via 192.168.100.1 dev wlo1 proto dhcp src 192.168.100.18 metric 600 
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown 
192.168.100.0/24 dev wlo1 proto kernel scope link src 192.168.100.18 metric 600 

```

```bash
dominik@Zenbook:~/Pulpit/DevOpsNotes/DevOps Notes$ resolvectl status
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (wlo1)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 192.168.100.1
       DNS Servers: 192.168.100.1
     Default Route: yes

Link 3 (docker0)
    Current Scopes: none
         Protocols: -DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
     Default Route: no

```

```bash
dominik@Zenbook:~/Pulpit/DevOpsNotes/DevOps Notes$ nmcli device status
DEVICE        TYPE      STATE                   CONNECTION     
wlo1          wifi      połączono               NETIASPOT-kpQ4 
lo            loopback  connected (externally)  lo             
docker0       bridge    connected (externally)  docker0   
```





1. Active network interface ✅
   1. `wlo1             UP             192.168.100.18/24 fe80::51a2:9770:bb50:3e8/64 `
2. Interface type ✅
   1. `wlo1          wifi      połączono               NETIASPOT-kpQ4 `
3. MAC address ✅
   1. `08:8e:90:b2:45:71`
4. IPv4 address ✅
   1. `192.168.100.18/24`
5. IPv6 address ✅
   1. `fe80::51a2:9770:bb50:3e8`
6. Default gateway ✅
   1. `default via 192.168.100.1 `
7. Default route ✅
   1. `default via 192.168.100.1 dev wlo1`
8. DNS server ✅
   1. `192.168.100.1`

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

```bash
Netid  State       Recv-Q  Send-Q         Local Address:Port       Peer Address:Port Process                                     
udp    ESTAB       0       0             192.168.100.18:42539      57.144.112.1:443   users:(("brave",pid=12584,fd=21)) 
```



Investigate:

1. Process name ✅ 
   1. `brave`
2. PID ✅
   1. `12584`
3. Protocol ✅
   1. `UDP`
4. Local IP ✅
   1. `192.168.100.18`
5. Local port ✅
   1. `:42539`
6. Remote IP ✅
   1. `57.144.112.1`
7. Remote port ✅
   1. `443`
8. Connection state ✅
   1. `ESTAB`

Then explain:

> Why is the local port different from the remote port?
> 
> The local port is a temporary source port chosen by the operating system, while the remote port is the destination port used by the remote service.

---

# Challenge 3 — Port Investigation

Choose any active connection from:

```bash
ss -tupn
```

```bash
Netid  State  Recv-Q  Send-Q           Local Address:Port        Peer Address:Port  Process                                      
udp    ESTAB  0       0               192.168.100.18:43065      188.114.96.11:443    users:(("brave",pid=12584,fd=102)) 
```



Then investigate its process.

Use:

```bash
ps -fp <PID>
```

```bash
UID          PID    PPID  C STIME TTY          TIME CMD
dominik    12584   12510  1 14:03 ?        00:01:30 /snap/brave/676/opt/brave.com/brave/brave --type=utility --utility-sub-type=n
```

and:

```bash
lsof -p <PID>
```

```bash
dominik@Zenbook:~$ lsof -p 12584
COMMAND   PID    USER  FD      TYPE             DEVICE  SIZE/OFF    NODE NAME
brave   12584 dominik cwd       DIR              259,2      4096 8650754 /home/dominik
brave   12584 dominik rtd       DIR               0,66       540       1 /
brave   12584 dominik txt       REG                7,2 318922048      25 /snap/brave/676/opt/brave.com/brave/brave
brave   12584 dominik DEL       REG               0,27             26234 /dev/shm/.org.chromium.Chromium.Pt0Z9A

```



```bash
dominik@Zenbook:~$ ps -p 12584 -o pid,comm,%cpu,%mem
    PID COMMAND         %CPU %MEM
  12584 brave            1.0  1.0

```



```bash
dominik@Zenbook:~$ ss -tupn | grep 12584
tcp   ESTAB 0      0           192.168.100.18:38620 192.168.100.14:8009 users:(("brave",pid=12584,fd=39))         
tcp   ESTAB 0      0           192.168.100.18:43372 172.64.155.209:443  users:(("brave",pid=12584,fd=22))         
tcp   ESTAB 0      0           192.168.100.18:50880 57.144.113.134:443  users:(("brave",pid=12584,fd=67))         
tcp   ESTAB 0      0           192.168.100.18:34782 57.144.112.141:443  users:(("brave",pid=12584,fd=70))         
tcp   ESTAB 0      0           192.168.100.18:51180 57.144.112.141:443  users:(("brave",pid=12584,fd=21))         
tcp   ESTAB 0      0           192.168.100.18:41154  140.82.114.25:443  users:(("brave",pid=12584,fd=29))         
tcp   ESTAB 0      0           192.168.100.18:55356 57.144.112.145:443  users:(("brave",pid=12584,fd=82))         
tcp   ESTAB 0      0           192.168.100.18:55370 57.144.112.145:443  users:(("brave",pid=12584,fd=78))         
tcp   ESTAB 0      0           192.168.100.18:55386 57.144.112.145:443  users:(("brave",pid=12584,fd=86))         
tcp   ESTAB 0      0           192.168.100.18:55400 57.144.112.145:443  users:(("brave",pid=12584,fd=99))         
tcp   ESTAB 0      0           192.168.100.18:59610 172.64.148.235:443  users:(("brave",pid=12584,fd=31)) 
```



Find:

1. Process name ✅
   1. `brave`
2. PID ✅
   1. `12584`
3. User ✅
   1. `dominik`
4. Parent PID ✅
   1. `12510`
5. CPU usage ✅
   1. `1.0`
6. Memory usage ✅
   1. `1.0`
7. Command ✅
   1. `/snap/brave/676/opt/brave.com/brave/brave --type=utility --utility-sub-type=n`
8. Open files ✅
   1. `lsof -p 12584`
9. Network connections ✅
   1. `TCP`

---

# Final Challenge — Network Investigation

Without looking at your notes, answer these questions:

1. What is a network interface?    
   1. `Something that lets a computer connect to a network, like Wi-Fi or Ethernet.`
2. What is a MAC address?
   1. `A physical address that identifies a network interface.`
3. What is an IP address?
   1. `An address used to identify a device on a network.`
4. What is the difference between IPv4 and IPv6?
   1. `IPv4 has shorter 32-bit addresses, while IPv6 has 128-bit addresses and many more possible addresses.`
5. What is `127.0.0.1`?
   1. `It's a localhost`
6. What is the loopback interface?
   1. `a virtual network interface that a computer or router uses to communicate with itself`
7. What is a default gateway?
   1. `A default gateway which machine use to connect to the internet`
8. What is a routing table?
   1. `It tells the computer where to send network packets.`
9. What does `ip route` show?
   1. `It shows the routing table and the default gateway`
10. What does `ping` test?
    1. `It checks if another device is reachable.`
11. What is DNS?
    1. `It translates domain names like `google.com` into IP addresses.`
12. What does `dig` do?
    1. `It checks DNS information.`
13. What is a port?
    1. `A number used to identify a network service or process.`
14. What is the difference between TCP and UDP?
    1. `TCP is reliable and checks that data arrives. UDP is faster/lighter but doesn't guarantee delivery.`
15. What does `ss` show?
    1. `It shows network connections and listening ports.`
16. What does `LISTEN` mean?
    1. `A service is waiting for incoming connections.`
17. What does `ESTAB` mean?
    1. `That the connection is estabilished`
18. What does `lsof -i :8080` do?
    1. `Shows which process is using port 8080.`
19. What is an ephemeral port?
    1. `A temporary port usually given to a client connection.`
20. How would you troubleshoot a Linux machine that cannot access the Internet?
    1. `Check the interface, IP address, gateway, routing, then test an IP like `8.8.8.8`, and finally check DNS.`
