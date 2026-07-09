# 🧪 Automation, Scheduling & Operations Practical Lab

This lab contains hands-on Linux automation tasks used by DevOps Engineers for managing production servers.

The goal is to practice environment management, cron automation, backups, monitoring, background jobs, and system services.

---

# 🛠️ Lab Environment

Tested with:

- Ubuntu Linux Server
- Bash Shell
- Terminal


Tools Used:

- Cron
- Bash Scripts
- Systemd
- Journalctl
- Tar
- Rsync
- Linux Monitoring Commands

---

# 🌍 Lab 1: Environment Variables


Create temporary variable:

```bash
export APP_ENV=production
```


Verify:

```bash
echo $APP_ENV
```


List environment variables:

```bash
env
```

---

# 📂 Lab 2: Permanent Environment Variable


Open bash configuration:

```bash
nano ~/.bashrc
```


Add:

```bash
export PROJECT=DevOps-Handbook
```


Reload:

```bash
source ~/.bashrc
```


Test:

```bash
echo $PROJECT
```

---

# ⏰ Lab 3: Create Cron Job


Open cron editor:

```bash
crontab -e
```


Add job:

```bash
* * * * * echo "Cron Running" >> /tmp/cron-test.log
```


Verify:

```bash
crontab -l
```


Check output:

```bash
cat /tmp/cron-test.log
```

---

# 💾 Lab 4: Backup Automation Script


Create script:

```bash
nano backup.sh
```


Script:

```bash
#!/bin/bash


DATE=$(date +%F)


mkdir -p backup


tar -czf backup/logs-$DATE.tar.gz /var/log


echo "Backup Completed"
```

---

# 🚀 Execute Backup


Permission:

```bash
chmod +x backup.sh
```


Run:

```bash
./backup.sh
```

---

# 🔄 Lab 5: Rsync Backup


Create folders:

```bash
mkdir source backup
```


Create test file:

```bash
echo "DevOps Backup Test" > source/file.txt
```


Sync:

```bash
rsync -av source/ backup/
```

---

# 📊 Lab 6: System Monitoring


Check CPU:

```bash
top
```


Check memory:

```bash
free -h
```


Check disk:

```bash
df -h
```


Check uptime:

```bash
uptime
```

---

# 🤖 Lab 7: Health Check Automation


Create:

```bash
nano health-check.sh
```


Script:

```bash
#!/bin/bash


echo "SERVER HEALTH REPORT"


echo "Hostname"

hostname


echo "Memory"

free -h


echo "Disk"

df -h


echo "Load"

uptime
```

Run:

```bash
chmod +x health-check.sh


./health-check.sh
```

---

# ⚙️ Lab 8: Background Jobs


Run background process:

```bash
sleep 500 &
```


View jobs:

```bash
jobs
```


Move foreground:

```bash
fg %1
```


Stop:

```bash
CTRL + C
```

---

# 🚀 Lab 9: Nohup Long Running Task


Run script after logout:

```bash
nohup ./health-check.sh &
```


Check output:

```bash
cat nohup.out
```

---

# 🔧 Lab 10: Systemd Service Management


Install nginx:

```bash
sudo apt install nginx -y
```


Start:

```bash
sudo systemctl start nginx
```


Enable:

```bash
sudo systemctl enable nginx
```


Status:

```bash
systemctl status nginx
```

---

# 📜 Lab 11: Service Logs


View logs:

```bash
journalctl -u nginx
```


Live logs:

```bash
journalctl -u nginx -f
```

---

# 🔥 Production Troubleshooting Scenario


Problem:

Application is down.


Step 1: Check service

```bash
systemctl status nginx
```


Step 2: Check logs

```bash
journalctl -u nginx
```


Step 3: Check resources

```bash
df -h

free -h
```


Step 4: Restart

```bash
sudo systemctl restart nginx
```

---

# 📸 Screenshot Checklist


Add screenshots:

```text
screenshots/

├── 01-environment-variable.png

├── 02-cron-automation.png

├── 03-backup-script.png

├── 04-health-monitoring.png

├── 05-background-job.png

└── 06-systemd-service.png
```

---

# 📌 Commands Practiced


| Command | Purpose |
|-|-|
| export | Environment variables |
| crontab | Schedule jobs |
| tar | Backup creation |
| rsync | File synchronization |
| top | Monitoring |
| free | Memory check |
| df | Disk usage |
| jobs | Background jobs |
| nohup | Persistent process |
| systemctl | Service control |
| journalctl | Logs |

---

# 🎯 Real DevOps Usage


These skills are used for:

✔ Production automation  
✔ Scheduled maintenance  
✔ Backup workflows  
✔ Server monitoring  
✔ Incident troubleshooting  
✔ Infrastructure operations  

---

# 🚀 Lab Completed

Automation, Scheduling & Linux Operations fundamentals successfully practiced for DevOps environments.
