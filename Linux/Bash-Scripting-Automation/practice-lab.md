# 🧪 Bash Scripting & Automation Practical Lab

This lab contains hands-on Bash scripting tasks focused on real-world DevOps automation.

The goal is to practice shell scripting, log analysis, server monitoring, backups, and automation workflows.

---

# 🛠️ Lab Environment

Tested with:

- Ubuntu Linux
- Bash Shell
- Terminal


Tools Used:

- Bash
- grep
- awk
- sed
- cron
- tar
- systemctl

---

# 🐚 Lab 1: Create Your First Bash Script


Create script:

```bash
touch hello-devops.sh
```


Open:

```bash
nano hello-devops.sh
```


Add:

```bash
#!/bin/bash

echo "Welcome to DevOps Automation"

date

whoami
```


Give permission:

```bash
chmod +x hello-devops.sh
```


Run:

```bash
./hello-devops.sh
```

---

# 📦 Lab 2: Variables & Arguments


Create:

```bash
nano deploy.sh
```


Script:

```bash
#!/bin/bash

APP=$1

echo "Deploying Application: $APP"
```


Run:

```bash
chmod +x deploy.sh

./deploy.sh nginx
```


Expected:

```text
Deploying Application: nginx
```

---

# 🔀 Lab 3: Conditions


Check file availability:

```bash
#!/bin/bash


FILE="/var/log/syslog"


if [ -f $FILE ]

then

echo "File Found"

else

echo "File Missing"

fi
```

---

# 🔁 Lab 4: Loop Automation


Create multiple folders:

```bash
#!/bin/bash


for folder in app logs backup

do

mkdir $folder

echo "$folder created"

done
```

---

# 🧩 Lab 5: Functions


Reusable function example:

```bash
#!/bin/bash


check_server(){

echo "Checking Server"

uptime

}


check_server
```

---

# 📄 Lab 6: Log Analysis


Find errors:

```bash
grep ERROR application.log
```


Ignore case:

```bash
grep -i error application.log
```


Count errors:

```bash
grep ERROR application.log | wc -l
```

---

# 📊 Lab 7: Text Processing


Extract columns:

```bash
awk '{print $1}' file.txt
```


Replace text:

```bash
sed 's/error/ERROR/g' app.log
```


Sort unique values:

```bash
sort file.txt | uniq
```

---

# 🖥️ Lab 8: Server Health Check Script


Create:

```bash
nano health-check.sh
```


Script:

```bash
#!/bin/bash


echo "===== SYSTEM REPORT ====="


echo "HOSTNAME"

hostname


echo "UPTIME"

uptime


echo "MEMORY"

free -h


echo "DISK"

df -h
```


Run:

```bash
chmod +x health-check.sh

./health-check.sh
```

---

# 💾 Lab 9: Backup Automation


Create:

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


Run:

```bash
./backup.sh
```

---

# 🔍 Lab 10: Service Monitoring


Monitor Nginx:

```bash
#!/bin/bash


SERVICE="nginx"


if systemctl is-active --quiet $SERVICE

then

echo "Service Running"

else

echo "Restarting Service"

sudo systemctl restart $SERVICE

fi
```

---

# 🌐 Lab 11: Website Status Check


Script:

```bash
#!/bin/bash


URL="https://google.com"


STATUS=$(curl -o /dev/null -s -w "%{http_code}" $URL)


echo "Status Code: $STATUS"
```

---

# ⏰ Lab 12: Schedule Script With Cron


Open cron:

```bash
crontab -e
```


Run backup every day:

```bash
0 1 * * * /home/user/backup.sh
```


Check cron jobs:

```bash
crontab -l
```

---

# 📸 Screenshot Checklist


Add screenshots:

```text
screenshots/

├── 01-script-execution.png
├── 02-variable-script.png
├── 03-grep-log-analysis.png
├── 04-awk-sed-output.png
├── 05-health-check-script.png
├── 06-backup-automation.png
└── 07-cron-job.png
```

---

# 📌 Commands Practiced


| Command | Purpose |
|-|-|
| chmod +x | Execute permission |
| bash | Run scripts |
| grep | Search logs |
| awk | Process text |
| sed | Modify text |
| tar | Backup archive |
| cron | Schedule scripts |
| systemctl | Service automation |


---

# 🎯 Real DevOps Usage


These automation skills are used for:

✔ Server health monitoring  
✔ Production troubleshooting  
✔ Backup automation  
✔ CI/CD scripts  
✔ Log analysis  
✔ Infrastructure management  


---

# 🚀 Lab Completed

Bash Scripting & Automation fundamentals successfully practiced for DevOps environments.
