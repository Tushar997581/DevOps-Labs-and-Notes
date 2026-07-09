# 🌐 Linux Network Troubleshooting for DevOps Engineers

Network troubleshooting is an essential skill for DevOps Engineers, Cloud Engineers, and System Administrators.

It helps diagnose connectivity issues, server failures, DNS problems, API errors, and production outages.

---

## 📌 Why Network Troubleshooting Matters?

In real-world environments, engineers troubleshoot:

- Server connectivity problems
- Application communication issues
- DNS failures
- Firewall problems
- Port availability
- API response issues

---

# 📡 Check Network Connectivity


## ping Command

`ping` verifies whether a server is reachable.

Syntax:

```bash
ping hostname
```

Example:

```bash
ping google.com
```

or

```bash
ping 8.8.8.8
```


Output shows:

- Packet loss
- Response time
- Connectivity status

---

# 🌍 Check IP Address


Display network interfaces:

```bash
ip address
```

Short command:

```bash
ip a
```


Example output:

```text
eth0

192.168.1.10
```


---

# 🛣️ Check Routing Table


View network routes:

```bash
ip route
```


or:

```bash
route -n
```


Shows:

- Default gateway
- Network routes
- Interfaces


---

# 🔌 Check Open Ports


## ss Command

Modern replacement for netstat.

Show listening ports:

```bash
ss -tulnp
```


Options:

```text
-t = TCP

-u = UDP

-l = Listening

-n = Numbers

-p = Process
```

---

# 📊 Netstat Command


Install:

```bash
sudo apt install net-tools -y
```


Check ports:

```bash
netstat -tulnp
```


Example:

Find Nginx:

```bash
netstat -tulnp | grep nginx
```

---

# 🌎 Test HTTP / API Connectivity


## curl Command


Check website response:

```bash
curl https://google.com
```


Show headers only:

```bash
curl -I https://google.com
```


Test API:

```bash
curl http://localhost:8080/api
```


---

# 🔎 DNS Troubleshooting


## nslookup


Find domain IP:

```bash
nslookup google.com
```


---

## dig Command


Install:

```bash
sudo apt install dnsutils -y
```


Check DNS:

```bash
dig google.com
```


Short output:

```bash
dig google.com +short
```


---

# 🚀 Trace Network Path


## traceroute


Install:

```bash
sudo apt install traceroute -y
```


Run:

```bash
traceroute google.com
```


Shows network path between servers.

---

# 🔥 Check Firewall


Ubuntu firewall:

```bash
sudo ufw status
```


Allow port:

```bash
sudo ufw allow 80
```


Allow SSH:

```bash
sudo ufw allow 22
```


---

# 🔍 Check Running Services


Example:

Check if Nginx is listening:

```bash
ss -tulnp | grep 80
```


Check SSH:

```bash
ss -tulnp | grep 22
```


---

# 🧪 Troubleshooting Scenario


## Problem:

Website is not opening.


Step 1: Check server:

```bash
ping server-ip
```


Step 2: Check service:

```bash
systemctl status nginx
```


Step 3: Check port:

```bash
ss -tulnp | grep 80
```


Step 4: Test locally:

```bash
curl localhost
```


Step 5: Check logs:

```bash
journalctl -u nginx
```


---

# ☁️ AWS EC2 Network Checks


## SSH Not Working


Check:

Security Group:

```text
Port 22 allowed
```

Instance status:

```bash
ping public-ip
```

SSH debug:

```bash
ssh -v ubuntu@server-ip
```


---

## Website Not Opening


Check ports:

HTTP:

```text
80
```

HTTPS:

```text
443
```


Check Nginx:

```bash
systemctl status nginx
```


---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| ping | Check connectivity |
| ip a | Show IP address |
| ip route | Routing table |
| ss -tulnp | Open ports |
| netstat | Network connections |
| curl | Test HTTP/API |
| nslookup | DNS lookup |
| dig | DNS debugging |
| traceroute | Network path |
| ufw status | Firewall check |


---

# 🎯 DevOps Use Cases


Network troubleshooting helps with:

✔ Debugging server issues  
✔ Fixing application downtime  
✔ AWS EC2 troubleshooting  
✔ Checking service connectivity  
✔ Production incident handling  


---

# 🚀 Skills Covered

- Linux Networking
- DNS Troubleshooting
- Port Management
- Server Debugging
- Cloud Networking
- DevOps Operations
