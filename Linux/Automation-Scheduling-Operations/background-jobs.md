# ⚙️ Background Jobs & Process Management for DevOps Engineers

Background job management is an important Linux skill used to run and control long-running processes.

DevOps Engineers use background processes for scripts, automation tasks, monitoring jobs, and production operations.

---

# 📌 What are Background Jobs?

A background job is a process that runs without blocking the terminal.

Used for:

- Long-running scripts
- Server tasks
- Monitoring processes
- Automation jobs
- Application execution

Example:

```text
Backup script running in background
Monitoring script collecting data
Long deployment process
```

---

# 🚀 Run Process in Background

Use `&` operator.

Example:

```bash
sleep 300 &
```

Output:

```text
[1] 12345
```

Meaning:

```text
[1]   → Job ID

12345 → Process ID
```

---

# 📋 View Background Jobs

Command:

```bash
jobs
```

Example output:

```text
[1]+ Running sleep 300 &
```

---

# 🔄 Bring Background Job to Foreground

Command:

```bash
fg
```

Using job ID:

```bash
fg %1
```

---

# ⏸️ Stop Running Foreground Process

Press:

```text
CTRL + Z
```

This pauses the process.

---

# ▶️ Resume Stopped Process in Background


Command:

```bash
bg
```


Example:

```bash
bg %1
```

---

# 🔥 Run Command After Logout (nohup)

Normally processes stop when SSH session closes.

`nohup` keeps processes running.


Syntax:

```bash
nohup command &
```


Example:

```bash
nohup ./backup.sh &
```

---

# 📄 nohup Output


Default output file:

```text
nohup.out
```


View output:

```bash
cat nohup.out
```

Live view:

```bash
tail -f nohup.out
```

---

# 🔍 Find Running Processes


List processes:

```bash
ps aux
```


Find process:

```bash
ps aux | grep script
```

---

# 🆔 Find Process ID


Using pidof:

```bash
pidof nginx
```


Using pgrep:

```bash
pgrep nginx
```

---

# ❌ Kill Background Process


Normal stop:

```bash
kill PID
```


Example:

```bash
kill 1234
```


Force stop:

```bash
kill -9 PID
```

---

# 📊 Monitor Processes


Using top:

```bash
top
```


Using htop:

```bash
htop
```

---

# 🧪 DevOps Example: Long Backup Job


Run backup:

```bash
nohup ./backup.sh &
```


Check:

```bash
jobs
```


Monitor:

```bash
tail -f nohup.out
```

---

# 🧪 DevOps Example: Background Monitoring


Script:

```bash
#!/bin/bash


while true

do

date

df -h

sleep 60

done
```


Run:

```bash
nohup ./monitor.sh &
```

---

# 🔥 Difference Between &, nohup, systemd


| Method | Usage |
|-|-|
| & | Run in background temporarily |
| nohup | Continue after logout |
| systemd | Permanent service management |


---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| command & | Start background job |
| jobs | Show jobs |
| fg | Move foreground |
| bg | Resume background |
| CTRL + Z | Pause process |
| nohup | Run after logout |
| ps aux | Show processes |
| kill | Stop process |
| top | Monitor process |


---

# 🎯 DevOps Use Cases


Background process management helps with:

✔ Running automation scripts  
✔ Long deployments  
✔ Server monitoring  
✔ Backup execution  
✔ Production maintenance  
✔ Remote server operations  


---

# 🚀 Skills Covered

- Background Jobs
- Linux Processes
- nohup Usage
- Job Control
- Process Monitoring
- DevOps Operations
