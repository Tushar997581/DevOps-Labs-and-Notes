# 📊 Linux System Monitoring for DevOps Engineers

System monitoring is an essential part of managing production infrastructure.

DevOps Engineers monitor servers to identify performance issues, prevent downtime, and maintain reliable applications.

---

# 📌 Why System Monitoring?

Monitoring helps detect:

- High CPU usage
- Memory issues
- Disk problems
- Service failures
- Application performance issues

Benefits:

✔ Faster troubleshooting  
✔ Better performance  
✔ Improved reliability  
✔ Early issue detection  

---

# 🖥️ CPU Monitoring


## top Command

Shows real-time system activity.

```bash
top
```

Displays:

- CPU usage
- Running processes
- Memory usage
- Load average


---

# 🚀 htop Command

Interactive monitoring tool.


Install:

```bash
sudo apt install htop -y
```


Run:

```bash
htop
```

Features:

- Process management
- CPU usage graph
- Memory usage view

---

# ⏱️ System Load Monitoring


Check uptime:

```bash
uptime
```


Example:

```text
load average: 0.20, 0.35, 0.40
```


Shows:

- 1 minute load
- 5 minute load
- 15 minute load

---

# 🧠 Memory Monitoring


Check RAM usage:

```bash
free -h
```


Example:

```text
Total   Used   Free

8GB     3GB    5GB
```

---

# 🔥 Find High Memory Processes


Command:

```bash
ps aux --sort=-%mem | head
```

Shows applications consuming the most RAM.

---

# ⚙️ CPU Consuming Processes


Find high CPU usage:

```bash
ps aux --sort=-%cpu | head
```

---

# 💾 Disk Monitoring


Check filesystem usage:

```bash
df -h
```


Example:

```text
Filesystem

/dev/sda1  60%
```

---

# 📂 Directory Size Monitoring


Check folder usage:

```bash
du -sh /var/log
```


Find large folders:

```bash
du -ah / | sort -rh | head
```

---

# 💿 Disk Devices


Show disks:

```bash
lsblk
```


Filesystem type:

```bash
df -T
```

---

# 🔍 Service Monitoring


Check service:

```bash
systemctl status nginx
```


Failed services:

```bash
systemctl --failed
```

---

# 📜 Log Monitoring


System logs:

```bash
journalctl
```


Service logs:

```bash
journalctl -u nginx
```


Live logs:

```bash
journalctl -f
```

---

# 🤖 Server Health Check Script


Create:

```bash
nano health-check.sh
```


Script:

```bash
#!/bin/bash


echo "===== SERVER HEALTH REPORT ====="


echo "Hostname"

hostname


echo "Uptime"

uptime


echo "Memory"

free -h


echo "Disk"

df -h


echo "Processes"

ps aux | head
```

---

# 🚀 Execute Script


Permission:

```bash
chmod +x health-check.sh
```


Run:

```bash
./health-check.sh
```

---

# 🚨 Disk Alert Script


Example:

```bash
#!/bin/bash


LIMIT=80


USAGE=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')


if [ $USAGE -gt $LIMIT ]

then

echo "Disk Usage Alert"

else

echo "Disk Normal"

fi
```

---

# ⏰ Automate Monitoring With Cron


Run health check every 10 minutes:

```bash
*/10 * * * * /home/user/health-check.sh
```

---

# 📌 Monitoring Tools


Common DevOps tools:

- Prometheus
- Grafana
- CloudWatch
- Nagios
- Zabbix


---

# 🧪 Practice Tasks


## Task 1: Monitor CPU

```bash
top
```


---

## Task 2: Check Memory

```bash
free -h
```


---

## Task 3: Check Disk

```bash
df -h
```


---

## Task 4: Analyze Logs

```bash
journalctl -f
```

---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| top | Process monitoring |
| htop | Advanced monitor |
| uptime | Load average |
| free -h | RAM usage |
| df -h | Disk usage |
| du -sh | Folder size |
| ps aux | Processes |
| journalctl | Logs |
| systemctl | Services |


---

# 🎯 DevOps Use Cases


System monitoring helps with:

✔ Production monitoring  
✔ Incident response  
✔ Performance tuning  
✔ Server troubleshooting  
✔ Capacity planning  
✔ Automation workflows  


---

# 🚀 Skills Covered

- Linux Monitoring
- Resource Management
- Log Analysis
- Health Checks
- Performance Troubleshooting
- Production Operations
