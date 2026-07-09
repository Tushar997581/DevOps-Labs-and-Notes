# ⏰ Cron Jobs & Task Scheduling for DevOps Engineers

Cron is a Linux scheduling system used to automatically execute commands and scripts at specific times.

DevOps Engineers use cron jobs to automate backups, monitoring, cleanup tasks, reports, and maintenance activities.

---

# 📌 What is Cron?

Cron helps automate:

- Backup jobs
- Health checks
- Log cleanup
- Monitoring scripts
- Report generation
- Maintenance tasks

Cron runs in the background using the `cron` service.

---

# 🔧 Check Cron Service


Check status:

```bash
systemctl status cron
```

Start cron:

```bash
sudo systemctl start cron
```

Enable after reboot:

```bash
sudo systemctl enable cron
```

---

# 📝 Manage Cron Jobs


Edit current user cron:

```bash
crontab -e
```


List cron jobs:

```bash
crontab -l
```


Remove all cron jobs:

```bash
crontab -r
```

---

# 🕒 Cron Syntax


Format:

```text
* * * * * command


| | | | |
| | | | |
| | | | └── Day of Week (0-7)
| | | └──── Month (1-12)
| | └────── Day (1-31)
| └──────── Hour (0-23)
└────────── Minute (0-59)
```

---

# 📌 Cron Schedule Examples


Every minute:

```bash
* * * * * /path/script.sh
```


Every 5 minutes:

```bash
*/5 * * * * /path/script.sh
```


Every hour:

```bash
0 * * * * /path/script.sh
```


Every day at 2 AM:

```bash
0 2 * * * /backup.sh
```


Every Sunday:

```bash
0 3 * * 0 /cleanup.sh
```

---

# 📤 Redirect Cron Output


Save logs:

```bash
0 2 * * * backup.sh >> /var/log/backup.log
```

Save errors:

```bash
0 2 * * * backup.sh >> backup.log 2>&1
```

---

# 🧪 Create Backup Cron Job


Create script:

```bash
nano backup.sh
```


Script:

```bash
#!/bin/bash


DATE=$(date +%F)


tar -czf backup-$DATE.tar.gz /var/log


echo "Backup Completed"
```


Permission:

```bash
chmod +x backup.sh
```


Schedule:

```bash
crontab -e
```


Add:

```bash
0 1 * * * /home/user/backup.sh
```

---

# 🖥️ Health Check Cron Example


Script:

```bash
#!/bin/bash


echo "Server Report"


uptime


free -h


df -h
```


Run every 10 minutes:

```bash
*/10 * * * * /home/user/health.sh
```

---

# 🧹 Log Cleanup Automation


Remove logs older than 7 days:

```bash
find /var/log -name "*.log" -mtime +7 -delete
```


Cron:

```bash
0 3 * * * find /var/log -name "*.log" -mtime +7 -delete
```

---

# 🔍 Check Cron Logs


Ubuntu:

```bash
grep CRON /var/log/syslog
```


Using journalctl:

```bash
journalctl -u cron
```

---

# ⚠️ Common Cron Problems


## Script Not Running


Check permission:

```bash
chmod +x script.sh
```


Use absolute path:

Wrong:

```bash
backup.sh
```


Correct:

```bash
/home/user/backup.sh
```

---

# 🌍 Environment Issue


Cron has limited environment variables.

Add PATH:

```bash
PATH=/usr/local/bin:/usr/bin:/bin
```

inside crontab.

---

# 🔥 Special Cron Keywords


| Keyword | Meaning |
|-|-|
| @reboot | Run after startup |
| @hourly | Every hour |
| @daily | Every day |
| @weekly | Every week |
| @monthly | Every month |


Example:

```bash
@reboot /home/user/start.sh
```

---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| crontab -e | Edit cron |
| crontab -l | List jobs |
| crontab -r | Remove jobs |
| systemctl status cron | Check cron |
| journalctl -u cron | View logs |


---

# 🎯 DevOps Use Cases


Cron is used for:

✔ Automated backups  
✔ Health monitoring  
✔ Log rotation  
✔ Database dumps  
✔ Security scans  
✔ Report generation  
✔ Maintenance automation  


---

# 🚀 Skills Covered

- Cron Scheduling
- Linux Automation
- Backup Jobs
- Monitoring Jobs
- Production Automation
- DevOps Operations
