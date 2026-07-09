
# 🐧 Linux System Administration

Linux is the foundation of modern DevOps, Cloud Infrastructure, and Server Management.

This section contains practical Linux administration concepts, commands, troubleshooting techniques, and real-world system management tasks used by DevOps Engineers.

---

## 📌 Topics Covered

### 🔹 Process Management

Understanding and controlling Linux processes.

Concepts:
- Running processes
- Process ID (PID)
- Foreground & background processes
- Job management
- Process signals

Commands:

```bash
ps aux

top

htop

jobs

kill <PID>

kill -9 <PID>
````

---

## 🔹 Systemd Service Management

Managing Linux services using systemd.

Tasks:

* Start services
* Stop services
* Restart services
* Enable services during boot
* Check service status

Commands:

```bash
sudo systemctl start nginx

sudo systemctl stop nginx

sudo systemctl restart nginx

sudo systemctl enable nginx

sudo systemctl status nginx
```

---

## 🔹 Logs & Troubleshooting

Analyzing system and application logs.

Commands:

```bash
journalctl

journalctl -u nginx

journalctl -f
```

Used for:

* Debugging service failures
* Checking application errors
* Monitoring system events

---

## 🔹 Disk Management

Checking storage and filesystem usage.

Commands:

```bash
df -h

du -sh /var/log

lsblk
```

---

## 🔹 Memory & Resource Monitoring

Monitor system performance.

Commands:

```bash
free -h

top

uptime
```

---

## 🧪 Hands-on Practice

Practical tasks completed:

✔ Installed Nginx web server
✔ Managed Nginx using systemctl
✔ Checked service logs
✔ Monitored CPU & Memory usage
✔ Analyzed disk utilization

---

## 🛠️ Tools Used

* Linux Terminal
* Ubuntu Server
* Bash Shell
* Systemd
* Journalctl
* Nginx

---

## 🎯 Learning Outcome

After completing this section:

✔ Understand Linux server operations
✔ Manage production services
✔ Troubleshoot failures using logs
✔ Monitor server resources
✔ Build strong DevOps fundamentals

---

## 🚀 Part of DevOps Engineer Handbook

Continuous learning of:

Linux → Networking → Automation → Docker → Kubernetes → Cloud → CI/CD

```

This README will make the folder look like **professional documentation**, not classroom notes.
```
