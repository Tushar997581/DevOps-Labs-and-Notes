# ⚙️ Automation Scripts for DevOps Engineers

Automation is a core responsibility of DevOps Engineers.

Bash automation scripts help reduce manual tasks, improve reliability, and manage production infrastructure efficiently.

---

# 📌 Why Automation?

Automation helps with:

- Server monitoring
- Application deployment
- Backup management
- Log cleanup
- Health checks
- System maintenance

Benefits:

✔ Saves time  
✔ Reduces manual errors  
✔ Improves consistency  
✔ Supports scalable operations  

---

# 🖥️ Server Health Check Script

This script checks:

- Host information
- CPU load
- Memory usage
- Disk usage

---

Create:

```bash
nano health-check.sh
```

Script:

```bash
#!/bin/bash

echo "===== SERVER HEALTH REPORT ====="

echo "Hostname:"
hostname


echo "Uptime:"
uptime


echo "Memory Usage:"
free -h


echo "Disk Usage:"
df -h


echo "Running Processes:"
ps aux | head
```

Give permission:

```bash
chmod +x health-check.sh
```

Run:

```bash
./health-check.sh
```

---

# 💾 Backup Automation Script

Automatically create compressed backups.

---

Create:

```bash
nano backup.sh
```

Script:

```bash
#!/bin/bash


SOURCE="/var/log"

DEST="/backup"

DATE=$(date +%F)


mkdir -p $DEST


tar -czf $DEST/log-backup-$DATE.tar.gz $SOURCE


echo "Backup Completed"
```

Run:

```bash
./backup.sh
```

---

# 🧹 Log Cleanup Automation


Delete old log files automatically.


Script:

```bash
#!/bin/bash


find /var/log -name "*.log" -mtime +7 -delete


echo "Old logs removed"
```

Uses:

- Prevent disk full issues
- Maintain server storage


---

# 🔍 Service Monitoring Script


Monitor application status.


Example: Nginx


```bash
#!/bin/bash


SERVICE="nginx"


if systemctl is-active --quiet $SERVICE

then

echo "$SERVICE is running"

else

echo "$SERVICE stopped"

systemctl restart $SERVICE

fi
```

Features:

✔ Checks service  
✔ Detects failure  
✔ Auto restart  

---

# 📊 Disk Alert Script


Monitor disk usage.


```bash
#!/bin/bash


LIMIT=80


USAGE=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')


if [ $USAGE -gt $LIMIT ]

then

echo "Disk Alert: $USAGE% used"

else

echo "Disk Normal"

fi
```

---

# 🚀 Deployment Automation Script


Example application deployment:


```bash
#!/bin/bash


echo "Starting Deployment"


git pull


docker compose down


docker compose up -d --build


echo "Deployment Completed"
```

---

# 🐳 Docker Container Check Script


```bash
#!/bin/bash


docker ps


if [ $? -eq 0 ]

then

echo "Docker Running"

else

echo "Docker Issue Found"

fi
```

---

# 🌐 Website Availability Checker


Check website status:


```bash
#!/bin/bash


URL="https://example.com"


STATUS=$(curl -o /dev/null -s -w "%{http_code}" $URL)


if [ $STATUS -eq 200 ]

then

echo "Website Online"

else

echo "Website Down"

fi
```

---

# ⏰ Schedule Automation Using Cron


Open cron:

```bash
crontab -e
```


Run script every day:

```bash
0 1 * * * /home/user/backup.sh
```


Run every 5 minutes:

```bash
*/5 * * * * /home/user/check.sh
```

---

# 📁 Recommended Script Structure


```text
scripts/

├── health-check.sh

├── backup.sh

├── service-monitor.sh

├── disk-alert.sh

└── deploy.sh
```

---

# 📌 Automation Commands Summary


| Command | Purpose |
|-|-|
| cron | Schedule tasks |
| tar | Create backups |
| find | Search/delete files |
| systemctl | Manage services |
| curl | Website testing |
| docker | Container automation |
| awk | Process output |
| sed | Modify text |


---

# 🎯 Real DevOps Usage


Automation scripts are used for:

✔ Production monitoring  
✔ CI/CD pipelines  
✔ Server maintenance  
✔ Cloud automation  
✔ Application deployment  
✔ Incident recovery  


---

# 🚀 Skills Covered

- Bash Automation
- Server Monitoring
- Backup Automation
- Deployment Scripts
- Cron Jobs
- Production Operations
