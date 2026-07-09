# 💾 Backup Automation for DevOps Engineers

Backup automation is an important practice for maintaining reliable infrastructure and preventing data loss.

DevOps Engineers automate backups for applications, databases, logs, and configuration files.

---

# 📌 Why Backup Automation?

Manual backups are:

- Time consuming
- Error prone
- Difficult to maintain at scale


Automation provides:

✔ Regular backups  
✔ Faster recovery  
✔ Consistency  
✔ Production reliability  

---

# 📦 Archive Files Using TAR

`tar` is used to combine files and directories into archives.

---

## Create Archive


Syntax:

```bash
tar -cf backup.tar folder/
```

Example:

```bash
tar -cf logs.tar /var/log
```

---

# 🗜️ Create Compressed Backup


Using gzip compression:

```bash
tar -czf backup.tar.gz /var/log
```


Meaning:

```text
-c = create

-z = gzip

-f = file
```

---

# 📂 Extract Backup


Extract tar.gz file:

```bash
tar -xzf backup.tar.gz
```

Extract to specific location:

```bash
tar -xzf backup.tar.gz -C /backup
```

---

# 🗓️ Backup With Date


Create backup filename using date:


```bash
DATE=$(date +%F)


tar -czf backup-$DATE.tar.gz /var/log
```


Example output:

```text
backup-2026-07-09.tar.gz
```

---

# 🤖 Automated Backup Script


Create script:

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


echo "Backup Completed Successfully"
```

---

# 🚀 Run Backup Script


Give permission:

```bash
chmod +x backup.sh
```


Execute:

```bash
./backup.sh
```

---

# 🔄 Rsync Backup Automation


Rsync synchronizes files efficiently.


Local backup:

```bash
rsync -av /app /backup/
```


Remote backup:

```bash
rsync -av /data user@server:/backup/
```

---

# 🔑 Rsync Using SSH Key


Example:

```bash
rsync -av \
-e "ssh -i key.pem" \
/data ubuntu@server:/backup/
```

---

# 🧹 Backup Retention Policy


Delete old backups automatically.


Remove backups older than 7 days:

```bash
find /backup \
-name "*.tar.gz" \
-mtime +7 \
-delete
```

---

# ⏰ Schedule Backup Using Cron


Open cron:

```bash
crontab -e
```


Run every day at 1 AM:

```bash
0 1 * * * /home/user/backup.sh
```

---

# 📝 Backup Logs


Save backup output:


```bash
0 1 * * * backup.sh >> backup.log 2>&1
```


Example log:

```text
Backup Completed Successfully
```

---

# 🗄️ Database Backup Example


MySQL backup:

```bash
mysqldump \
-u root \
-p database_name > backup.sql
```


Compress:

```bash
gzip backup.sql
```

---

# ☁️ Cloud Backup Example


AWS S3 sync:

```bash
aws s3 sync /backup s3://bucket-name
```


Used for:

- Offsite backup
- Disaster recovery
- Long term storage

---

# 🧪 Practice Lab


## Task 1

Create backup directory:

```bash
mkdir backup
```


---

## Task 2

Backup logs:

```bash
tar -czf logs.tar.gz /var/log
```


---

## Task 3

Create automation script:

```bash
nano backup.sh
```

---

## Task 4

Schedule with cron:

```bash
crontab -e
```

---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| tar | Create archive |
| gzip | Compress files |
| rsync | Sync backups |
| find | Remove old backups |
| cron | Schedule backup |
| mysqldump | Database backup |
| aws s3 sync | Cloud backup |


---

# 🎯 DevOps Use Cases


Backup automation is used for:

✔ Application backups  
✔ Log backups  
✔ Database backups  
✔ Disaster recovery  
✔ Cloud storage backups  
✔ Production maintenance  


---

# 🚀 Skills Covered

- Backup Strategy
- Bash Automation
- Cron Scheduling
- Rsync
- Data Recovery
- DevOps Operations


