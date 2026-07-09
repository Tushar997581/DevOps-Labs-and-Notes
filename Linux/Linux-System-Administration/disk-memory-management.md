# 💾 Linux Disk & Memory Management

Disk and memory management are important Linux administration skills required for maintaining reliable servers.

DevOps Engineers monitor storage, memory usage, and system resources to prevent failures and improve performance.

---

## 📌 Why Disk & Memory Monitoring Matters?

In production environments:

- Applications generate logs
- Databases store large amounts of data
- Services consume RAM and CPU resources
- Low disk or memory can crash applications

Regular monitoring helps maintain system health.

---

# 💽 Disk Management

Disk management involves checking:

- Available storage
- Mounted filesystems
- Disk partitions
- Directory usage


---

# 📊 Check Disk Usage


## df Command

Shows filesystem disk space usage:

```bash
df
```

Human-readable format:

```bash
df -h
```


Example:

```text
Filesystem   Size   Used   Available
/dev/sda1     50G    20G      30G
```

---

# 📁 Check Directory Size


## du Command


Check folder size:

```bash
du -sh /var/log
```


Check all directories:

```bash
du -h
```


Find large folders:

```bash
du -ah / | sort -rh | head
```


---

# 💿 Block Device Management


List storage devices:

```bash
lsblk
```


Shows:

- Disk name
- Size
- Partitions
- Mount points


Example:

```text
NAME    SIZE   MOUNTPOINT

sda      50G

└─sda1   50G   /
```


---

# 🔗 Mounted Filesystems


View mounted devices:

```bash
mount
```


Better format:

```bash
findmnt
```


---

# 📌 Disk Information


Check disk partitions:

```bash
sudo fdisk -l
```


Check filesystem:

```bash
df -T
```


---

# 🧹 Cleaning Disk Space


Remove package cache:

Ubuntu:

```bash
sudo apt clean
```


Remove unused packages:

```bash
sudo apt autoremove
```


---

# 🧠 Memory Management


Memory monitoring helps identify:

- High RAM usage
- Application memory leaks
- Performance issues


---

# 📊 Check RAM Usage


## free Command


Display memory:

```bash
free
```


Human-readable:

```bash
free -h
```


Example:

```text
Total    Used    Free

8GB      4GB     4GB
```


---

# ⚙️ Process Memory Usage


Using top:

```bash
top
```


Sort processes by memory:

Press:

```text
Shift + M
```


---

# 🚀 Advanced Process Monitor


Install htop:

```bash
sudo apt install htop -y
```


Run:

```bash
htop
```


Shows:

- CPU usage
- RAM usage
- Running processes


---

# 🔥 Find High Memory Processes


Command:

```bash
ps aux --sort=-%mem | head
```


Shows applications consuming most RAM.


---

# 🔄 Swap Memory


Check swap:

```bash
swapon --show
```


Memory + swap:

```bash
free -h
```


---

# 📈 System Performance


Check uptime:

```bash
uptime
```


Shows:

- Running time
- Logged users
- Load average


---

# 🧪 Practical Tasks


## Task 1: Check Server Storage

```bash
df -h
```


---

## Task 2: Find Large Logs

```bash
du -sh /var/log/*
```


---

## Task 3: Monitor RAM

```bash
free -h
```


---

## Task 4: Find Resource Heavy Process

```bash
top
```

or

```bash
ps aux --sort=-%mem | head
```


---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| df -h | Disk usage |
| du -sh | Folder size |
| lsblk | Block devices |
| fdisk -l | Disk partitions |
| mount | Mounted filesystem |
| free -h | Memory usage |
| top | Resource monitoring |
| htop | Advanced monitor |
| uptime | Load average |


---

# 🎯 DevOps Use Cases


Disk & Memory Management helps with:

✔ Server health monitoring  
✔ Preventing disk failures  
✔ Debugging performance issues  
✔ Managing cloud instances  
✔ Production troubleshooting  


---

# 🚀 Skills Covered

- Linux Storage Management
- Resource Monitoring
- Server Optimization
- Performance Analysis
- DevOps Troubleshooting
