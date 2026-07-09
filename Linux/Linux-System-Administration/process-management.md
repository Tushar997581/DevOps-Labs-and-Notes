# ⚙️ Linux Process Management

Process management is one of the core responsibilities of Linux System Administrators and DevOps Engineers.

Every running application, command, or service in Linux runs as a process. Understanding how to monitor and control processes helps in troubleshooting and managing production servers.

---

## 📌 What is a Process?

A process is an active instance of a running program.

Examples:

- Web Server (Nginx, Apache)
- Database Server
- Shell Commands
- Background Jobs
- Applications

Every process has a unique:

- PID (Process ID)
- User Owner
- CPU Usage
- Memory Usage
- Current State


---

# 🔍 Viewing Running Processes


## ps Command

Display running processes:

```bash
ps
```

Show all processes:

```bash
ps aux
```

Example:

```bash
ps aux | grep nginx
```

Used for finding a specific running process.

---

# 📊 Real-Time Process Monitoring


## top Command

Shows live system processes:

```bash
top
```

Displays:

- CPU usage
- Memory usage
- Running processes
- System load


---

## htop Command

Interactive process monitoring tool.

Install:

Ubuntu:

```bash
sudo apt install htop -y
```

Run:

```bash
htop
```

Features:

- Easy process view
- CPU/Memory bars
- Kill processes directly


---

# 🆔 Finding Process ID (PID)

Using pidof:

```bash
pidof nginx
```

Using pgrep:

```bash
pgrep nginx
```


Example:

```bash
ps aux | grep ssh
```


---

# ❌ Killing Processes


## Normal Termination

```bash
kill PID
```

Example:

```bash
kill 1234
```


---

## Force Kill Process

```bash
kill -9 PID
```

Example:

```bash
kill -9 1234
```

SIGKILL immediately stops the process.


---

# 🚦 Process Signals

Common Linux signals:


| Signal | Number | Usage |
|-|-|-|
| SIGTERM | 15 | Gracefully stop process |
| SIGKILL | 9 | Force stop process |
| SIGHUP | 1 | Reload process |


Example:

```bash
kill -15 PID
```


---

# 🔄 Background & Foreground Jobs


Run command in background:

```bash
sleep 300 &
```


View background jobs:

```bash
jobs
```


Move job to foreground:

```bash
fg %1
```


Move stopped process background:

```bash
bg %1
```


---

# 🔎 Process Tree


View parent-child process relationship:

```bash
pstree
```


or:

```bash
ps -ef
```


---

# 📈 System Load


Check server uptime:

```bash
uptime
```


Example output:

```text
load average: 0.15, 0.20, 0.18
```


Shows:

- 1 minute load
- 5 minute load
- 15 minute load


---

# 🧪 Practice Tasks


## Task 1

Start a background process:

```bash
sleep 500 &
```


Check:

```bash
jobs
```


---

## Task 2

Find process:

```bash
ps aux | grep sleep
```


---

## Task 3

Kill process:

```bash
kill <PID>
```


---

# 🛠️ Commands Summary


| Command | Purpose |
|-|-|
| ps aux | List processes |
| top | Live monitoring |
| htop | Advanced monitoring |
| kill | Stop process |
| jobs | Show background jobs |
| fg | Bring job foreground |
| bg | Continue in background |
| pstree | Process hierarchy |
| uptime | System load |


---

# 🎯 DevOps Use Cases

Process management helps with:

✔ Debugging application issues  
✔ Finding high CPU processes  
✔ Restarting failed services  
✔ Server performance monitoring  
✔ Production troubleshooting  


---

# 🚀 Skills Covered

- Linux Administration
- Server Monitoring
- Troubleshooting
- Resource Management
- DevOps Operations
