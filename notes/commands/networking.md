# 🌐 Linux Networking

> Commands for inspecting network interfaces, connections, routes, DNS and network services.

---

## 📡 Network interfaces

### `ip`

The `ip` command is used to view and configure network interfaces, addresses and routing.

List network interfaces:

```bash
ip link
```

Show interfaces and their IP addresses:

```bash
ip addr
```

Short version:

```bash
ip a
```

💡 `ip a` is one of the first commands to run when checking a machine's network configuration.

---

### Show a specific interface

```bash
ip addr show eth0
```

---

### Show the routing table

```bash
ip route
```

Short version:

```bash
ip r
```

Example:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0
```

The `default` route indicates where traffic is sent when there is no more specific route.

---

## 🔎 Connectivity

### `ping`

Tests whether another host is reachable using ICMP.

```bash
ping <IP>
```

Example:

```bash
ping 192.168.1.1
```

Limit the number of packets:

```bash
ping -c 4 192.168.1.1
```

💡 A failed ping does **not necessarily** mean that a host is offline. ICMP may simply be blocked.

---

### `traceroute`

Shows the path packets take to reach a destination.

```bash
traceroute <host>
```

Example:

```bash
traceroute google.com
```

On some systems you may need to install it first.

---

## 🔌 Ports & connections

### `ss`

Displays network sockets, connections and listening ports.

Show listening TCP and UDP ports:

```bash
ss -tuln
```

Useful options:

```text
-t   → TCP
-u   → UDP
-l   → Listening
-n   → Don't resolve service names
```

Show processes associated with sockets:

```bash
sudo ss -tulpn
```

💡 This is particularly useful when checking which services are listening on a machine.

---

### Common `ss` combinations

```bash
ss -tln
```

Listening TCP ports.

```bash
ss -uln
```

Listening UDP ports.

```bash
ss -tun
```

Active TCP and UDP connections.

---

## 🌍 DNS

### `nslookup`

Queries DNS information.

```bash
nslookup <domain>
```

Example:

```bash
nslookup example.com
```

---

### `dig`

A more detailed DNS query tool.

```bash
dig <domain>
```

Example:

```bash
dig example.com
```

Request a specific record:

```bash
dig example.com A
dig example.com MX
dig example.com TXT
```

Useful for DNS enumeration and troubleshooting.

---

## 🌐 Network requests

### `curl`

Transfers data to or from a server.

Basic request:

```bash
curl <URL>
```

Example:

```bash
curl http://example.com
```

Show HTTP response headers:

```bash
curl -I http://example.com
```

Follow redirects:

```bash
curl -L http://example.com
```

Download a file:

```bash
curl -O http://example.com/file.txt
```

💡 `curl` is extremely useful in HTB for interacting with web servers directly from the terminal.

---

### `wget`

Downloads files from the web.

```bash
wget <URL>
```

Example:

```bash
wget http://example.com/file.txt
```

Download and save with a specific filename:

```bash
wget -O file.txt http://example.com/file.txt
```

---

## 🖥️ Host information

### `hostname`

Displays the machine's hostname.

```bash
hostname
```

Show the IP address associated with the hostname:

```bash
hostname -I
```

---

### `getent`

Can query information from the system's configured databases.

For example, resolve a hostname:

```bash
getent hosts example.com
```

It can also be useful for checking how the system resolves names.

---

## 🗺️ Network configuration files

Some important files related to networking:

```text
/etc/hosts
```

Local hostname resolution.

```text
/etc/resolv.conf
```

DNS resolver configuration.

```text
/etc/hostname
```

System hostname.

Example:

```bash
cat /etc/hosts
cat /etc/resolv.conf
cat /etc/hostname
```

💡 `/etc/hosts` is particularly interesting during HTB labs because it is commonly used to associate custom hostnames with IP addresses.

---

## 🧪 Basic network reconnaissance

When starting to investigate a Linux machine, these commands provide a quick overview:

### 1. Check interfaces

```bash
ip a
```

### 2. Check routes

```bash
ip r
```

### 3. Check listening ports

```bash
sudo ss -tulpn
```

### 4. Check DNS configuration

```bash
cat /etc/resolv.conf
```

### 5. Check local hostname resolution

```bash
cat /etc/hosts
```

### 6. Test connectivity

```bash
ping -c 4 <IP>
```

---

## 🧠 Quick reference

| Command      | What it does                            |
| ------------ | --------------------------------------- |
| `ip a`       | 📡 Show interfaces and IP addresses     |
| `ip r`       | 🗺️ Show routing table                  |
| `ping`       | 📶 Test connectivity                    |
| `traceroute` | 🛣️ Trace network path                  |
| `ss`         | 🔌 Show connections and listening ports |
| `nslookup`   | 🌍 Query DNS                            |
| `dig`        | 🔎 Perform detailed DNS queries         |
| `curl`       | 🌐 Make HTTP/network requests           |
| `wget`       | 📥 Download files                       |
| `hostname`   | 🖥️ Show hostname                       |
| `getent`     | 🔍 Query system databases               |

---

## 🧩 Useful options to remember

```text
ip a
    → Interfaces + IP addresses

ip r
    → Routing table

ss -tuln
    → Listening TCP/UDP ports

sudo ss -tulpn
    → Listening ports + processes

ping -c 4 <IP>
    → Send 4 ICMP packets

curl -I <URL>
    → Show HTTP headers

curl -L <URL>
    → Follow redirects

dig <domain>
    → DNS query
```

---

### 🔗 Related topics

* `services.md` → System services
* `processes.md` → Running processes
* `filesystem.md` → Files and directories
* `permissions.md` → Permissions and ownership
