# ⚙️ Automation, Scheduling & Linux Operations for DevOps Engineers

Automation is the foundation of DevOps Engineering.

This section focuses on automating Linux administration tasks, scheduling jobs, managing environments, monitoring systems, and operating production servers efficiently.

---

# 📌 Topics Covered

- Environment Variables
- Cron Job Scheduling
- Backup Automation
- System Monitoring
- Background Processes
- Systemd Service Management
- Production Automation Scripts

---

# 🌍 Environment Variables

Environment variables store configuration values used by:

- Operating Systems
- Applications
- Docker Containers
- Kubernetes Pods
- CI/CD Pipelines


View variables:

```bash
env
```

Print variable:

```bash
echo $PATH
```

Create variable:

```bash
export APP_ENV=production
```

---

# 📁 Environment Configuration Files


## .bashrc

Used for interactive shell configuration.

```bash
nano ~/.bashrc
```

Example:

```bash
export APP_ENV=production
```

Apply:

```bash
source ~/.bashrc
```

---

## .env File Example


Application configuration:

```env
APP_ENV=production

DATABASE_URL=mysql://server:3306/app

SECRET_KEY=mysecret
```

---

# ⏰ Cron Job Automation

Cron schedules commands and scripts automatically.

Used for:

- Backups
- Reports
- Cleanup jobs
- Monitoring scripts

---

## Edit Cron Jobs


```bash
crontab -e
```


List jobs:

```bash
crontab -l
```

Remove jobs:

```bash
crontab -r
```

---

# 🕒 Cron Syntax


```text
* * * * * command


| | | | |
| | | | |
| | | | └── Day of Week
| | | └──── Month
| | └────── Day
| └──────── Hour
└────────── Minute
```

---

# 📌 Cron Examples


Every minute:

```bash
* * * * * script.sh
```


Every day at 2 AM:

```bash
0 2 * * * backup.sh
```


Every Sunday:

```bash
0 3 * * 0 cleanup.sh
```

---

# 💾 Backup Automation


Backups protect production data.

Common tools:

- tar
- gzip
- rsync


---

# 📦 Create Archive


```bash
tar -czf backup.tar.gz /var/log
```


Extract:

```bash
tar -xzf backup.tar.gz
```

---

# 🔄 Rsync Backup


Local backup:

```bash
rsync -av /app /backup
```


Remote backup:

```bash
rsync -av /data user@server:/backup
```

---

# 🖥️ System Monitoring


Monitor server resources.

---

## CPU


```bash
top
```


```bash
htop
```


---

## Memory


```bash
free -h
```


---

## Disk Usage


```bash
df -h
```


Directory size:

```bash
du -sh /var/log
```

---

# ⚙️ Background Job Management


Run process in background:

```bash
command &
```


View jobs:

```bash
jobs
```


Bring to foreground:

```bash
fg %1
```


Continue background:

```bash
bg %1
```

---

# 🚀 Keep Process Running After Logout


Using nohup:

```bash
nohup script.sh &
```


Output:

```text
nohup.out
```

---

# 🔧 Systemd Service Management


Systemd manages Linux services.

Examples:

- nginx
- docker
- ssh
- databases


---

# Start Service


```bash
sudo systemctl start nginx
```

---

# Stop Service


```bash
sudo systemctl stop nginx
```

---

# Restart Service


```bash
sudo systemctl restart nginx
```

---

# Enable on Boot


```bash
sudo systemctl enable nginx
```

---

# Check Status


```bash
systemctl status nginx
```

---

# 📜 View Service Logs


```bash
journalctl -u nginx
```


Live logs:

```bash
journalctl -u nginx -f
```

---

# 🧪 Real DevOps Automation Workflow


Example Production Flow:

```text
Application Server

        |
        |

Health Check Script

        |
        |

Cron Scheduler

        |
        |

Logs + Alerts

        |
        |

Backup Automation
```

---

# 🛠️ Tools Used


- Bash
- Cron
- Systemd
- Journalctl
- Tar
- Rsync
- Linux Monitoring Tools


---

# 🎯 DevOps Use Cases


These concepts are used for:

✔ Production server automation  
✔ Application monitoring  
✔ Backup scheduling  
✔ Incident troubleshooting  
✔ CI/CD automation  
✔ Cloud server operations  


---

# 🚀 Skills Covered

- Linux Automation
- Cron Scheduling
- Environment Management
- Backup Operations
- Process Management
- Service Management
- Production Monitoring


---

# 📚 DevOps Engineer Handbook Path


Linux Administration  
⬇️  
Networking & SSH  
⬇️  
Bash Scripting  
⬇️  
Automation & Operations  
⬇️  
Docker  
⬇️  
Kubernetes  
⬇️  
Cloud & CI/CD 🚀
