# 🔐 SSH Management for DevOps Engineers

SSH (Secure Shell) is one of the most important tools used by DevOps Engineers and System Administrators.

SSH allows secure remote access and management of Linux servers over an encrypted connection.

---

## 📌 What is SSH?

SSH stands for **Secure Shell**.

It is a network protocol used to securely connect with remote systems.

SSH is used for:

- Remote server administration
- Cloud instance access
- Running commands remotely
- Secure file transfers
- Automation workflows


Examples:

- AWS EC2 Login
- Linux Server Management
- CI/CD Deployments
- Infrastructure Automation

---

# ⚙️ How SSH Works

SSH uses a Client-Server architecture.

```
User Machine
      |
      | SSH Connection (Port 22)
      |
Remote Linux Server
```

Components:

- SSH Client → Initiates connection
- SSH Server → Accepts connection


Default SSH Port:

```text
22
```

---

# 🖥️ Basic SSH Connection


Syntax:

```bash
ssh username@server-ip
```


Example:

```bash
ssh ubuntu@192.168.1.20
```


AWS EC2 Example:

```bash
ssh -i key.pem ubuntu@public-ip
```

---

# 🔍 Check SSH Installation


Check SSH client:

```bash
ssh -V
```


Check SSH service:

```bash
systemctl status ssh
```


or

```bash
systemctl status sshd
```

---

# 🚀 Install SSH Server


Ubuntu:

```bash
sudo apt update

sudo apt install openssh-server -y
```


Start SSH:

```bash
sudo systemctl start ssh
```


Enable after reboot:

```bash
sudo systemctl enable ssh
```


---

# 📊 SSH Service Management


Restart SSH:

```bash
sudo systemctl restart ssh
```


Stop SSH:

```bash
sudo systemctl stop ssh
```


Check status:

```bash
sudo systemctl status ssh
```


---

# ⚙️ SSH Configuration File


Main configuration:

```bash
/etc/ssh/sshd_config
```


Open file:

```bash
sudo nano /etc/ssh/sshd_config
```


---

# 🔧 Common SSH Configurations


Change default SSH port:

```text
Port 2222
```


Disable root login:

```text
PermitRootLogin no
```


Disable password authentication:

```text
PasswordAuthentication no
```


Restart after changes:

```bash
sudo systemctl restart ssh
```

---

# 📝 SSH Client Configuration


Client config location:

```bash
~/.ssh/config
```


Example:

```text
Host production

    HostName 10.0.1.50

    User ubuntu

    IdentityFile ~/.ssh/id_rsa
```


Now connect:

```bash
ssh production
```


Benefits:

✔ No need to remember IP  
✔ Faster server access  
✔ Useful with multiple servers  

---

# 🧪 Running Remote Commands


Run command without login:

```bash
ssh user@server "uptime"
```


Example:

```bash
ssh ubuntu@server-ip "df -h"
```


---

# 🔎 Check Active SSH Connections


Using who:

```bash
who
```


Using ss:

```bash
ss -tnp
```


---

# 📂 Important SSH Files


| File | Purpose |
|-|-|
| ~/.ssh/id_rsa | Private key |
| ~/.ssh/id_rsa.pub | Public key |
| ~/.ssh/authorized_keys | Allowed keys |
| ~/.ssh/config | Client config |
| /etc/ssh/sshd_config | Server config |


---

# 🛡️ SSH Security Best Practices


✔ Use SSH keys instead of passwords  

✔ Disable root login  

✔ Change default SSH port if required  

✔ Keep private keys secure  

✔ Use firewall rules  

✔ Allow only trusted users  


---

# 🛠️ Troubleshooting SSH Issues


## Permission Denied Error


Check key permission:

```bash
chmod 400 key.pem
```


Connect again:

```bash
ssh -i key.pem user@ip
```


---

## Connection Refused


Check SSH service:

```bash
systemctl status ssh
```


Check port:

```bash
ss -tulnp | grep ssh
```


---

# 📌 Command Summary


| Command | Usage |
|-|-|
| ssh user@ip | Connect server |
| ssh -i key.pem | Login using key |
| ssh -V | Check SSH version |
| systemctl status ssh | SSH status |
| who | Active users |
| ss -tnp | Connections |


---

# 🎯 DevOps Use Cases


SSH helps DevOps Engineers with:

✔ AWS EC2 Management  
✔ Remote troubleshooting  
✔ Server configuration  
✔ CI/CD deployments  
✔ Infrastructure automation  


---

# 🚀 Skills Covered

- SSH Administration
- Linux Server Access
- Secure Authentication
- Remote Management
- Production Operations
