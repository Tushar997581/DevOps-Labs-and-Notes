# 🔧 Linux Systemd Service Management

Systemd is the default service manager used in modern Linux distributions.

DevOps Engineers use systemd to manage applications, background services, startup processes, and troubleshoot production systems.

---

## 📌 What is Systemd?

Systemd is responsible for:

- Starting system services
- Managing background processes
- Controlling application lifecycle
- Managing boot processes
- Monitoring service status

Examples of systemd managed services:

- Nginx
- Apache
- Docker
- SSH
- Database Services


---

# ⚙️ systemctl Command

`systemctl` is used to interact with systemd services.

Basic syntax:

```bash
systemctl [option] service-name
```

Example:

```bash
systemctl status nginx
```

---

# ▶️ Start a Service

Start a stopped service:

```bash
sudo systemctl start nginx
```

Example:

```bash
sudo systemctl start docker
```

Used when:

- Application is stopped
- Starting server processes manually


---

# ⏹️ Stop a Service

Stop a running service:

```bash
sudo systemctl stop nginx
```

Used before:

- Maintenance
- Configuration changes
- Troubleshooting


---

# 🔄 Restart a Service

Restart service after configuration changes:

```bash
sudo systemctl restart nginx
```

Example:

```bash
sudo systemctl restart ssh
```

---

# ♻️ Reload a Service

Reload configuration without stopping service:

```bash
sudo systemctl reload nginx
```

Useful for production environments to avoid downtime.


---

# 📊 Check Service Status

View current service health:

```bash
sudo systemctl status nginx
```

Shows:

- Active / Inactive status
- Process ID
- Memory usage
- Recent logs


Example output:

```text
Active: active (running)
Main PID: 1452
```

---

# 🚀 Enable Service at Boot

Automatically start service after reboot:

```bash
sudo systemctl enable nginx
```

Example:

```bash
sudo systemctl enable docker
```


---

# 🛑 Disable Startup Service

Prevent automatic startup:

```bash
sudo systemctl disable nginx
```


---

# 📋 List Services


Show all services:

```bash
systemctl list-units --type=service
```


Show running services:

```bash
systemctl --type=service --state=running
```


---

# 🔍 Service Logs with Journalctl


View service logs:

```bash
journalctl -u nginx
```


Show latest logs:

```bash
journalctl -u nginx -n 50
```


Live logs:

```bash
journalctl -u nginx -f
```


---

# 🧪 Hands-on Lab: Manage Nginx Service


## Step 1: Install Nginx

Ubuntu:

```bash
sudo apt update

sudo apt install nginx -y
```


---

## Step 2: Start Service

```bash
sudo systemctl start nginx
```


---

## Step 3: Check Status

```bash
sudo systemctl status nginx
```


---

## Step 4: Enable Auto Start

```bash
sudo systemctl enable nginx
```


---

## Step 5: Check Logs

```bash
journalctl -u nginx
```


---

# 🛠️ Common Troubleshooting


## Service Failed

Check status:

```bash
systemctl status service-name
```


Check logs:

```bash
journalctl -u service-name
```


---

## Restart Failed Service

```bash
sudo systemctl restart service-name
```


---

# 📂 Important Systemd Locations


| Path | Purpose |
|-|-|
| /etc/systemd/system | Custom service files |
| /lib/systemd/system | Default service files |
| /var/log | Application logs |


---

# 📌 Command Summary


| Command | Usage |
|-|-|
| systemctl start | Start service |
| systemctl stop | Stop service |
| systemctl restart | Restart service |
| systemctl reload | Reload config |
| systemctl status | Check service |
| systemctl enable | Start on boot |
| systemctl disable | Disable startup |
| journalctl -u | View logs |


---

# 🎯 DevOps Use Cases

Systemd knowledge helps with:

✔ Managing production applications  
✔ Deploying services  
✔ Troubleshooting failures  
✔ Checking server health  
✔ Automating infrastructure operations  


---

# 🚀 Skills Covered

- Linux Service Management
- System Administration
- Application Operations
- Production Troubleshooting
- DevOps Fundamentals
