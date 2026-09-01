# Linux Networking — Commands

## 1. Network Interfaces

| Command                        | What it does                                 | Example                        |
| ------------------------------ | -------------------------------------------- | ------------------------------ |
| `ip addr`                      | Shows network interfaces and IP addresses    | `ip addr`                      |
| `ip -br addr`                  | Shows interfaces and IPs in a compact format | `ip -br addr`                  |
| `ip link`                      | Shows network interfaces and their state     | `ip link`                      |
| `ip -s link`                   | Shows interface statistics                   | `ip -s link`                   |
| `ip link show <INTERFACE>`     | Shows information about one interface        | `ip link show enp2s0`          |
| `ip link set <INTERFACE> up`   | Brings an interface up                       | `sudo ip link set enp2s0 up`   |
| `ip link set <INTERFACE> down` | Brings an interface down                     | `sudo ip link set enp2s0 down` |

---

## 2. IP Addresses

| Command                    | What it does                         | Example               |
| -------------------------- | ------------------------------------ | --------------------- |
| `ip addr show`             | Shows all IP addresses               | `ip addr show`        |
| `ip addr show <INTERFACE>` | Shows IP addresses for one interface | `ip addr show enp2s0` |
| `ip -4 addr`               | Shows IPv4 addresses                 | `ip -4 addr`          |
| `ip -6 addr`               | Shows IPv6 addresses                 | `ip -6 addr`          |

---

## 3. Routing

| Command             | What it does                                     | Example                |
| ------------------- | ------------------------------------------------ | ---------------------- |
| `ip route`          | Shows the routing table                          | `ip route`             |
| `ip route show`     | Shows the routing table                          | `ip route show`        |
| `ip route get <IP>` | Shows which route Linux would use to reach an IP | `ip route get 8.8.8.8` |
| `ip neigh`          | Shows the neighbor/ARP table                     | `ip neigh`             |

### Useful routing information

| Output             | Meaning                      |
| ------------------ | ---------------------------- |
| `default via ...`  | Default gateway/route        |
| `dev enp2s0`       | Network interface being used |
| `src 192.168.1.10` | Source IP Linux will use     |
| `192.168.1.0/24`   | Directly connected network   |

---

## 4. Connectivity

| Command             | What it does                       | Example                 |
| ------------------- | ---------------------------------- | ----------------------- |
| `ping <HOST>`       | Tests connectivity to a host       | `ping 8.8.8.8`          |
| `ping -c 4 <HOST>`  | Sends a specific number of packets | `ping -c 4 8.8.8.8`     |
| `tracepath <HOST>`  | Shows the network path to a host   | `tracepath google.com`  |
| `traceroute <HOST>` | Traces the path to a host          | `traceroute google.com` |

### Recommended connectivity checks

| Test        | Command           | What it checks                    |
| ----------- | ----------------- | --------------------------------- |
| Loopback    | `ping 127.0.0.1`  | Local TCP/IP stack                |
| Gateway     | `ping <GATEWAY>`  | Local network connectivity        |
| Internet IP | `ping 8.8.8.8`    | Internet connectivity without DNS |
| Domain      | `ping google.com` | Connectivity + DNS resolution     |

---

## 5. DNS

| Command                     | What it does                                | Example                       |
| --------------------------- | ------------------------------------------- | ----------------------------- |
| `resolvectl status`         | Shows DNS configuration                     | `resolvectl status`           |
| `resolvectl query <DOMAIN>` | Resolves a domain using the system resolver | `resolvectl query google.com` |
| `dig <DOMAIN>`              | Performs a DNS query                        | `dig google.com`              |
| `dig <DOMAIN> +short`       | Shows a short DNS result                    | `dig google.com +short`       |
| `nslookup <DOMAIN>`         | Performs a DNS lookup                       | `nslookup google.com`         |

### Useful `dig` examples

| Command                   | Purpose                          |
| ------------------------- | -------------------------------- |
| `dig google.com`          | Basic DNS query                  |
| `dig google.com A`        | Query IPv4 address               |
| `dig google.com AAAA`     | Query IPv6 address               |
| `dig google.com MX`       | Query mail servers               |
| `dig google.com NS`       | Query authoritative name servers |
| `dig @8.8.8.8 google.com` | Query a specific DNS server      |

---

## 6. Ports and Sockets

| Command     | What it does                                   | Example     |
| ----------- | ---------------------------------------------- | ----------- |
| `ss -tulpn` | Shows listening TCP/UDP sockets with processes | `ss -tulpn` |
| `ss -tupn`  | Shows TCP/UDP connections with processes       | `ss -tupn`  |
| `ss -ltn`   | Shows listening TCP sockets                    | `ss -ltn`   |
| `ss -lun`   | Shows listening UDP sockets                    | `ss -lun`   |
| `ss -an`    | Shows all sockets in numeric form              | `ss -an`    |
| `ss -tlnp`  | Shows listening TCP sockets + processes        | `ss -tlnp`  |

### `ss` options

| Option | Meaning             |
| ------ | ------------------- |
| `-t`   | TCP                 |
| `-u`   | UDP                 |
| `-l`   | Listening           |
| `-a`   | All sockets         |
| `-p`   | Process information |
| `-n`   | Numeric output      |

---

## 7. Finding a Process Using a Port

| Command                     | What it does                           | Example                   |
| --------------------------- | -------------------------------------- | ------------------------- |
| `lsof -i :<PORT>`           | Finds processes using a specific port  | `lsof -i :8080`           |
| `ss -tulpn \| grep :<PORT>` | Searches socket information for a port | `ss -tulpn \| grep :8080` |
| `lsof -i TCP:<PORT>`        | Finds TCP users of a port              | `lsof -i TCP:8080`        |
| `lsof -i UDP:<PORT>`        | Finds UDP users of a port              | `lsof -i UDP:8080`        |

---

## 8. `lsof` — Open Files and Network Resources

| Command          | What it does                           | Example           |
| ---------------- | -------------------------------------- | ----------------- |
| `lsof`           | Shows open files/resources             | `lsof`            |
| `lsof -p <PID>`  | Shows resources opened by a process    | `lsof -p 22076`   |
| `lsof -i`        | Shows network-related open resources   | `lsof -i`         |
| `lsof -i :8080`  | Shows processes using port 8080        | `lsof -i :8080`   |
| `lsof -u <USER>` | Shows files/resources opened by a user | `lsof -u dominik` |

---

## 9. Network Interface Information

| Command                    | What it does                          | Example               |
| -------------------------- | ------------------------------------- | --------------------- |
| `ip link`                  | Interface state and MAC addresses     | `ip link`             |
| `ip addr`                  | Interface state, MAC and IP addresses | `ip addr`             |
| `ip -s link`               | RX/TX statistics and errors           | `ip -s link`          |
| `ip link show <INTERFACE>` | Information about one interface       | `ip link show enp2s0` |

Look for:

```text
link/ether
```

for the MAC address.

---

## 10. NetworkManager Commands

On systems using NetworkManager:

| Command                 | What it does                          | Example                 |
| ----------------------- | ------------------------------------- | ----------------------- |
| `nmcli device status`   | Shows network devices and their state | `nmcli device status`   |
| `nmcli connection show` | Shows network connections             | `nmcli connection show` |
| `nmcli device show`     | Shows detailed device information     | `nmcli device show`     |
| `nmcli general status`  | Shows NetworkManager status           | `nmcli general status`  |

---

## 11. Useful Filtering

| Command                    | What it does                     |
| -------------------------- | -------------------------------- |
| `ss -tulpn \| grep :80`    | Find services using port 80      |
| `ss -tulpn \| grep :443`   | Find services using port 443     |
| `ip addr \| grep inet`     | Show IP address lines            |
| `ip route \| grep default` | Show the default route           |
| `ip link \| grep state`    | Show interface states            |
| `lsof -i \| grep LISTEN`   | Find listening network resources |

---

## 12. Common Troubleshooting Commands

| Problem                     | First command to use |
| --------------------------- | -------------------- |
| No network interface        | `ip link`            |
| Interface is down           | `ip link`            |
| No IP address               | `ip addr`            |
| Wrong IP address            | `ip addr`            |
| No default gateway          | `ip route`           |
| Cannot reach gateway        | `ping <GATEWAY>`     |
| Cannot reach Internet       | `ping 8.8.8.8`       |
| IP works but domain doesn't | `dig google.com`     |
| DNS configuration problem   | `resolvectl status`  |
| Service not reachable       | `ss -tulpn`          |
| Port already in use         | `lsof -i :<PORT>`    |
| Need to find route to host  | `ip route get <IP>`  |
| Packet/path problem         | `tracepath <HOST>`   |

---

# Command Cheat Sheet

| Category               | Command               |
| ---------------------- | --------------------- |
| Interfaces             | `ip addr`             |
| Compact interfaces     | `ip -br addr`         |
| Interface state        | `ip link`             |
| Interface statistics   | `ip -s link`          |
| Routing table          | `ip route`            |
| Route to host          | `ip route get <IP>`   |
| Neighbor table         | `ip neigh`            |
| Connectivity           | `ping <HOST>`         |
| Network path           | `tracepath <HOST>`    |
| DNS configuration      | `resolvectl status`   |
| DNS query              | `dig <DOMAIN>`        |
| Short DNS query        | `dig <DOMAIN> +short` |
| Listening ports        | `ss -tulpn`           |
| TCP connections        | `ss -tupn`            |
| Open files/resources   | `lsof`                |
| Process resources      | `lsof -p <PID>`       |
| Port owner             | `lsof -i :<PORT>`     |
| NetworkManager devices | `nmcli device status` |

---

# Troubleshooting Flow

```text
1. Check interface
   ↓
ip link

2. Check IP address
   ↓
ip addr

3. Check routing
   ↓
ip route

4. Test gateway
   ↓
ping <GATEWAY>

5. Test Internet without DNS
   ↓
ping 8.8.8.8

6. Test DNS
   ↓
dig google.com

7. Check service/port
   ↓
ss -tulpn
```

# 
