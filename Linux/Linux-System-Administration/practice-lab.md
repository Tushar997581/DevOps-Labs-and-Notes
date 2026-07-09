# 🧪 Linux System Administration Practical Lab

This lab contains hands-on Linux Administration tasks focused on real-world DevOps server operations.

The goal is to practice service management, process monitoring, logging, and resource troubleshooting.

---

# 🛠️ Lab Environment

Tested on:

- Ubuntu Server
- Linux Terminal
- Bash Shell


Tools:

- systemctl
- journalctl
- Nginx
- Process monitoring tools

---

# 🚀 Lab 1: Install & Manage Nginx Service


## Step 1: Update System Packages

```bash
sudo apt update
```

---

## Step 2: Install Nginx

```bash
sudo apt install nginx -y
```

---

## Step 3: Start Nginx Service

```bash
sudo systemctl start nginx
```

---

## Step 4: Check Service Status

```bash
sudo systemctl status nginx
```

Expected:

```text
Active: active (running)
```

---

## Step 5: Enable Service After Reboot

```bash
sudo systemctl enable nginx
```

---

# 🔄 Lab 2: Service Operations


Restart service:

```bash
sudo systemctl restart nginx
```


Stop service:

```bash
sudo systemctl stop nginx
```


Start again:

```bash
sudo systemctl start nginx
```


Check failed services:

```bash
systemctl --failed
```

---

# ⚙️ Lab 3: Process Management


View running processes:

```bash
ps aux
```


Find Nginx process:

```bash
ps aux | grep nginx
```


Check process ID:

```bash
pidof nginx
```


Monitor processes:

```bash
top
```

or

```bash
htop
```

---

# 🔥 Lab 4: Background Process Management


Create background process:

```bash
sleep 500 &
```


Check background jobs:

```bash
jobs
```


Bring process foreground:

```bash
fg %1
```


Stop process:

```bash
kill <PID>
```


Force stop:

```bash
kill -9 <PID>
```

---

# 📊 Lab 5: Logs & Troubleshooting


View Nginx logs:

```bash
journalctl -u nginx
```


Latest logs:

```bash
journalctl -u nginx -n 20
```


Live monitoring:

```bash
journalctl -u nginx -f
```


Search errors:

```bash
journalctl | grep error
```

---

# 💾 Lab 6: Disk Monitoring


Check disk usage:

```bash
df -h
```


Check directory size:

```bash
du -sh /var/log
```


List disks:

```bash
lsblk
```


Mounted filesystem:

```bash
findmnt
```

---

# 🧠 Lab 7: Memory Monitoring


Check RAM:

```bash
free -h
```


System load:

```bash
uptime
```


Find high memory process:

```bash
ps aux --sort=-%mem | head
```

---

# 🧹 Lab 8: Basic Server Cleanup


Clean package cache:

```bash
sudo apt clean
```


Remove unused packages:

```bash
sudo apt autoremove
```

---

# 📝 Troubleshooting Scenario


## Problem:

Nginx service is not responding.


## Step 1: Check service

```bash
systemctl status nginx
```


## Step 2: Analyze logs

```bash
journalctl -u nginx
```


## Step 3: Restart service

```bash
sudo systemctl restart nginx
```


## Step 4: Verify

```bash
systemctl status nginx
```

---

# 📸 Screenshots Checklist


Add practical screenshots:

```
screenshots/

├── nginx-status.png
├── process-monitoring.png
├── journalctl-logs.png
├── disk-monitoring.png
└── memory-monitoring.png
```

---

# ✅ Skills Practiced


✔ Linux Service Management  
✔ Process Handling  
✔ Log Analysis  
✔ Disk Monitoring  
✔ Memory Monitoring  
✔ Troubleshooting Workflow  


---

# 🎯 Real DevOps Usage


These skills are used for:

- Production server management
- Application troubleshooting
- Cloud instance monitoring
- Incident debugging
- Infrastructure operations


---

# 🚀 Lab Completed

Linux System Administration fundamentals successfully practiced.
