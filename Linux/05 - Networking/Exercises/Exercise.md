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

```bash
dominik@Zenbook:~$ ip neigh

192.168.100.8 dev wlo1 FAILED 
fe80::1 dev wlo1 lladdr 14:46:58:45:c8:39 router REACHABLE 
```

Find:

1. At least one local network device ✅
   1. `fe80::1 dev wlo1`
2. Its IP address ✅
   1. `fe80::1`
3. Its MAC address ✅
   1. `14:46:58:45:c8:39`
4. Its state ✅
   1. `REACHABLE `

```
For a better understanding of `ip neigh`, please refer to `notes.md`.
```

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

```shell
dominik@Zenbook:~$ ping -c 4 192.168.100.1
PING 192.168.100.1 (192.168.100.1) 56(84) bytes of data.
64 bytes from 192.168.100.1: icmp_seq=1 ttl=64 time=4.44 ms
64 bytes from 192.168.100.1: icmp_seq=2 ttl=64 time=3.20 ms
64 bytes from 192.168.100.1: icmp_seq=3 ttl=64 time=3.26 ms
64 bytes from 192.168.100.1: icmp_seq=4 ttl=64 time=3.16 ms

--- 192.168.100.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 3.158/3.513/4.435/0.533 ms
dominik@Zenbook:~$ ping -c 4 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=114 time=16.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=114 time=16.4 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=114 time=16.4 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=114 time=16.6 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 16.373/16.557/16.790/0.167 ms
dominik@Zenbook:~$ ping -c 4 google.com
PING google.com (142.250.109.102) 56(84) bytes of data.
64 bytes from zr-in-f102.1e100.net (142.250.109.102): icmp_seq=1 ttl=112 time=11.7 ms
64 bytes from zr-in-f102.1e100.net (142.250.109.102): icmp_seq=2 ttl=112 time=11.5 ms
64 bytes from zr-in-f102.1e100.net (142.250.109.102): icmp_seq=3 ttl=112 time=13.1 ms
64 bytes from zr-in-f102.1e100.net (142.250.109.102): icmp_seq=4 ttl=112 time=13.4 ms

--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 11.479/12.415/13.368/0.844 ms
dominik@Zenbook:~$ 
```

Record:

- Does each test succeed?
  
  - `Yes each test have succeed`

- What does each test tell you?
  
  - `192.168.100.1 tells me that my computer can communicate with the local network and reach my router.`
  - `8.8.8.8 confirms my computer can access the internet`
  - `google.com confirms that DNS resolution and Internet connectivity are working correctly.`

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

```bash
dominik@Zenbook:~$ resolvectl status
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
dominik@Zenbook:~$ dig google.com +short
142.250.109.139
142.250.109.102
142.250.109.113
142.250.109.100
142.250.109.138
142.250.109.101
```

Find:

1. DNS server ✅
   1. `DNS Servers: 192.168.100.1`
2. Resolved IP address ✅
   1. `***DNS resolves a domain name into an IP address.`***
   2. `142.250.109.139
      142.250.109.102
      142.250.109.113
      142.250.109.100
      142.250.109.138
      142.250.109.101`
3. Network interface used by the DNS configuration ✅
   1. `Link 2(wlo1)`

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

```shell
dominik@Zenbook:~$ ping -c 4 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=114 time=16.5 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=114 time=16.3 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=114 time=16.5 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=114 time=16.2 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 16.192/16.391/16.538/0.145 ms
dominik@Zenbook:~$ ping -c 4 google.com
PING google.com (142.250.109.101) 56(84) bytes of data.
64 bytes from zr-in-f101.1e100.net (142.250.109.101): icmp_seq=1 ttl=110 time=12.1 ms
64 bytes from zr-in-f101.1e100.net (142.250.109.101): icmp_seq=2 ttl=110 time=13.5 ms
64 bytes from zr-in-f101.1e100.net (142.250.109.101): icmp_seq=3 ttl=110 time=13.4 ms
64 bytes from zr-in-f101.1e100.net (142.250.109.101): icmp_seq=4 ttl=110 time=13.3 ms

--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 12.103/13.074/13.482/0.565 ms
```

Answer:

1. Does the IP address work? ✅
   1. `Yes it does.`
2. Does the domain name work? ✅
   1. `Yes it does`
3. What would it mean if the IP worked but the domain did not? ✅
   1. `It could mean that my internet connectivity is okay but there could be a problem with DNS resolution`

---

## Exercise 12 — Listening Ports

Display listening TCP and UDP sockets.

```bash
ss -tulpn
```

```shell
dominik@Zenbook:~/Pulpit/DevOpsNotes/DevOps Notes$ ss -tulpn
Netid State  Recv-Q  Send-Q                     Local Address:Port   Peer Address:Port Process                             
udp   UNCONN 0       0                            224.0.0.251:5353        0.0.0.0:*     users:(("brave",pid=10701,fd=52))  
udp   UNCONN 0       0                            224.0.0.251:5353        0.0.0.0:*     users:(("brave",pid=10646,fd=247)) 
udp   UNCONN 0       0                                0.0.0.0:5353        0.0.0.0:*                                        
udp   UNCONN 0       0                             127.0.0.54:53          0.0.0.0:*                                        
udp   UNCONN 0       0                          127.0.0.53%lo:53          0.0.0.0:*                                        
udp   UNCONN 0       0                              127.0.0.1:323         0.0.0.0:*                                        
udp   UNCONN 0       0                                   [::]:5353           [::]:*                                        
udp   UNCONN 0       0                                  [::1]:323            [::]:*                                        
udp   UNCONN 0       0        [fe80::51a2:9770:bb50:3e8]%wlo1:546            [::]:*                                        
tcp   LISTEN 0       4096                          127.0.0.54:53          0.0.0.0:*                                        
tcp   LISTEN 0       4096                       127.0.0.53%lo:53          0.0.0.0:*                                        
tcp   LISTEN 0       128                            127.0.0.1:5939        0.0.0.0:*                                        
tcp   LISTEN 0       4096                           127.0.0.1:631         0.0.0.0:*                                        
tcp   LISTEN 0       4096                               [::1]:631            [::]:*     
```

Find:

1. One TCP listening port ✅
   1. `tcp   LISTEN 0       4096                          127.0.0.54:53          0.0.0.0:*`
2. One UDP listening port, if available ✅
   1. `udp   UNCONN 0       0                            224.0.0.251:5353        0.0.0.0:*     users:(("brave",pid=10701,fd=52))`
3. Process name ✅
   1. `users:(("brave",pid=10701,fd=52))`
   2. `So the process name = brave`
4. PID ✅
   1. `pid=10701`
5. Local address ✅
   1. `224.0.0.251:5353`
6. Port number ✅
   1. `5353`

```
FOR MORE INFO, PLEASE REFER TO NOTES.MD.
```

---

## Exercise 13 — Active Connections

Display active TCP and UDP connections.

```bash
ss -tupn
```

Choose one `ESTAB` connection.



```bash
dominik@Zenbook:~$ ss -tupn
Netid              State                    Recv-Q               Send-Q                                   Local Address:Port                                Peer Address:Port              Process                                                 
udp                ESTAB                    0                    0                                  192.168.100.18%wlo1:68                                 192.168.100.1:67                                                                        
udp                ESTAB                    0                    0                                       192.168.100.18:50039                              188.114.97.11:443                users:(("brave",pid=7925,fd=90))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:54404                             57.144.112.145:443                users:(("brave",pid=7925,fd=127))                      
tcp                ESTAB                    0                    0                                       192.168.100.18:54410                             57.144.112.145:443                users:(("brave",pid=7925,fd=31))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:54418                             57.144.112.145:443                users:(("brave",pid=7925,fd=73))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:54426                             57.144.112.145:443                users:(("brave",pid=7925,fd=79))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:38718                              140.82.114.25:443                users:(("brave",pid=7925,fd=51))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:38496                               104.18.86.42:443                users:(("brave",pid=7925,fd=63))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:38506                               104.18.86.42:443                users:(("brave",pid=7925,fd=102))                      
tcp                ESTAB                    0                    0                                       192.168.100.18:55118                             185.125.188.36:443                users:(("gnome-software",pid=5787,fd=41))              
tcp                CLOSE-WAIT               78                   0                                       192.168.100.18:57328                              50.112.66.242:443                users:(("brave",pid=7925,fd=37))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:42798                              104.18.41.158:443                users:(("brave",pid=7925,fd=57))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:52674                               104.18.32.47:443                users:(("brave",pid=7925,fd=27))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:46842                               104.18.39.21:443                users:(("brave",pid=7925,fd=38))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:58754                              54.189.76.203:443                users:(("brave",pid=7925,fd=45))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:52262                             57.144.112.141:443                users:(("brave",pid=7925,fd=85))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:52270                             57.144.112.141:443                users:(("brave",pid=7925,fd=65))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:53948                             57.144.113.134:443                users:(("brave",pid=7925,fd=30))                       
tcp                ESTAB                    0                    0                                       192.168.100.18:39928                              146.75.117.91:443                users:(("gnome-software",pid=5787,fd=46))   
```

`udp                ESTAB                    0                    0                                       192.168.100.18:50039                              188.114.97.11:443                users:(("brave",pid=7925,fd=90))  `

Find:

1. Protocol ✅
   1. `UDP`
2. State ✅
   1. `ESTAB`
3. Local IP ✅
   1. `192.168.100.18`
4. Local port ✅
   1. `50039`
5. Remote IP ✅
   1. `188.114.97.11`
6. Remote port ✅
   1. `443`
7. Process name ✅
   1. `brave`
8. PID ✅
   1. `pid=7925`

Explain which port is local and which port is remote.

```
Local port 50039 — is the port used by my computer for this connection.
Remote port 443 — is the port used by the remote computer or server.
```





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

1. **What does `LISTEN` mean?** 
   `It means that the program is waiting for incoming connections.`

2. **What does `ESTAB` mean?** 
   `It means that the connection is established.`

3. **Why can an `ESTAB` connection appear in `ss -tupn` but not in `ss -tulpn`?** 
   `ss -tupn shows active connections, while ss -tulpn shows ports that are waiting for incoming connections.`

4. **What is the difference between a listening port and a local ephemeral port?** 
   `A listening port is a port where a program waits for incoming connections, while an ephemeral port is a temporary port used by my computer to make outgoing connections.`

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
