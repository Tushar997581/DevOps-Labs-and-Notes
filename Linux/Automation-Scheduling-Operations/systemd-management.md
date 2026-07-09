# 🔧 Systemd Management for DevOps Engineers

Systemd is the default service manager used in modern Linux systems.

DevOps Engineers use systemd to manage applications, background services, startup processes, logs, and production workloads.

---

# 📌 What is Systemd?

Systemd manages:

- System startup
- Background services
- Application processes
- Service dependencies
- Logging

Examples:

- Nginx
- Docker
- SSH
- Jenkins
- Database services

---

# ⚙️ systemctl Command

`systemctl` is the command-line tool used to control systemd services.

Syntax:

```bash
systemctl action service-name
```

Example:

```bash
systemctl status nginx
```

---

# ▶️ Start Service


Start application:

```bash
sudo systemctl start nginx
```

Example:

```bash
sudo systemctl start docker
```

---

# ⏹️ Stop Service


Stop running service:

```bash
sudo systemctl stop nginx
```

---

# 🔄 Restart Service


Restart after configuration changes:

```bash
sudo systemctl restart nginx
```

---

# ♻️ Reload Service


Reload configuration without stopping:

```bash
sudo systemctl reload nginx
```

Useful for production servers.

---

# 📊 Check Service Status


Command:

```bash
systemctl status nginx
```


Output example:

```text
Active: active (running)

Main PID: 1520
```

Shows:

- Running status
- Process ID
- Recent logs

---

# 🚀 Enable Service on Boot


Automatically start after reboot:

```bash
sudo systemctl enable nginx
```

---

# 🛑 Disable Auto Startup


Command:

```bash
sudo systemctl disable nginx
```

---

# 📋 List Services


All services:

```bash
systemctl list-units --type=service
```


Running services:

```bash
systemctl --type=service --state=running
```

---

# ❌ Failed Services


Check failures:

```bash
systemctl --failed
```


Troubleshoot:

```bash
journalctl -u service-name
```

---

# 📜 Systemd Logs (Journalctl)


View all logs:

```bash
journalctl
```


Specific service:

```bash
journalctl -u nginx
```


Last 50 logs:

```bash
journalctl -u nginx -n 50
```


Live logs:

```bash
journalctl -u nginx -f
```

---

# 🛠️ Create Custom Systemd Service


Example:

Create script:

```bash
sudo nano /usr/local/bin/monitor.sh
```


Script:

```bash
#!/bin/bash


while true

do

echo "Service Running"

sleep 10

done
```


Permission:

```bash
sudo chmod +x /usr/local/bin/monitor.sh
```

---

# 📁 Create Service File


Location:

```bash
/etc/systemd/system/
```


Create:

```bash
sudo nano /etc/systemd/system/monitor.service
```


Service:

```ini
[Unit]

Description=Monitoring Service


[Service]

ExecStart=/usr/local/bin/monitor.sh

Restart=always


[Install]

WantedBy=multi-user.target
```

---

# 🔄 Reload Systemd


After creating service:

```bash
sudo systemctl daemon-reload
```

---

# ▶️ Start Custom Service


```bash
sudo systemctl start monitor
```


Check:

```bash
systemctl status monitor
```

---

# 🚀 Enable Custom Service


```bash
sudo systemctl enable monitor
```

Now service starts automatically after reboot.

---

# 🧪 DevOps Example Workflow


Deploy Application:

```text
Application Code

      ↓

Systemd Service

      ↓

Auto Restart

      ↓

Journal Logs

      ↓

Monitoring
```

---

# 📂 Important Locations


| Location | Purpose |
|-|-|
| /etc/systemd/system | Custom services |
| /lib/systemd/system | Default services |
| /var/log/journal | Logs |


---

# 🔥 Troubleshooting


Service not starting:

Check:

```bash
systemctl status app
```


View errors:

```bash
journalctl -u app
```


Reload changes:

```bash
systemctl daemon-reload
```

---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| systemctl start | Start service |
| systemctl stop | Stop service |
| systemctl restart | Restart |
| systemctl enable | Boot startup |
| systemctl status | Check health |
| systemctl --failed | Failed services |
| journalctl -u | Service logs |
| daemon-reload | Reload configs |


---

# 🎯 DevOps Use Cases


Systemd is used for:

✔ Running production applications  
✔ Auto restarting services  
✔ Managing Docker/Jenkins  
✔ Background workers  
✔ Server automation  
✔ Troubleshooting incidents  


---

# 🚀 Skills Covered

- Linux Service Management
- Custom Systemd Services
- Process Automation
- Logs Troubleshooting
- Production Operations
- 
