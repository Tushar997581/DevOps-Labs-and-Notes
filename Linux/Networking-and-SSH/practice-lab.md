# 🧪 Networking & SSH Practical Lab

This lab contains hands-on practice for SSH management, secure authentication, file transfer, and Linux network troubleshooting.

These tasks simulate real DevOps activities performed on cloud servers and production environments.

---

# 🛠️ Lab Environment

Tested with:

- Ubuntu Linux Server
- SSH Client
- Remote Linux Machine
- Terminal

Tools Used:

- OpenSSH
- SCP
- Rsync
- Curl
- Network Utilities

---

# 🔐 Lab 1: SSH Server Setup


## Step 1: Install SSH Server

Ubuntu:

```bash
sudo apt update

sudo apt install openssh-server -y
```

---

## Step 2: Start SSH Service

```bash
sudo systemctl start ssh
```

---

## Step 3: Enable SSH After Reboot

```bash
sudo systemctl enable ssh
```

---

## Step 4: Verify SSH Status

```bash
sudo systemctl status ssh
```

Expected:

```text
Active: active (running)
```

---

# 🖥️ Lab 2: Remote Server Connection


Basic SSH login:

```bash
ssh username@server-ip
```

Example:

```bash
ssh ubuntu@192.168.1.50
```

---

# 🔑 Lab 3: SSH Key Authentication


Generate SSH key:

```bash
ssh-keygen -t rsa -b 4096
```


Verify generated keys:

```bash
ls ~/.ssh
```


Output:

```text
id_rsa

id_rsa.pub
```

---

# 📤 Copy SSH Key to Server


Command:

```bash
ssh-copy-id username@server-ip
```


Test passwordless login:

```bash
ssh username@server-ip
```

---

# 🔒 Lab 4: Secure SSH Permissions


Set private key permission:

```bash
chmod 600 ~/.ssh/id_rsa
```


For AWS PEM keys:

```bash
chmod 400 server-key.pem
```

---

# ☁️ Lab 5: AWS EC2 SSH Connection


Connect EC2 instance:

```bash
ssh -i key.pem ubuntu@public-ip
```


Example:

```bash
ssh -i devops.pem ubuntu@13.20.10.50
```

---

# ⚙️ Lab 6: SSH Config Alias


Create config file:

```bash
nano ~/.ssh/config
```


Example:

```text
Host production

    HostName 10.0.1.50

    User ubuntu

    IdentityFile ~/.ssh/id_rsa
```


Connect:

```bash
ssh production
```

---

# 📂 Lab 7: Transfer Files Using SCP


Local → Remote:

```bash
scp test.txt user@server:/home/user/
```


Remote → Local:

```bash
scp user@server:/home/user/test.txt .
```


Transfer folder:

```bash
scp -r project/ user@server:/home/user/
```

---

# 🔄 Lab 8: File Synchronization Using Rsync


Sync directory:

```bash
rsync -av project/ user@server:/backup/
```


Show progress:

```bash
rsync -av --progress file.txt user@server:/backup/
```

---

# 🌐 Lab 9: Network Troubleshooting


Check connectivity:

```bash
ping google.com
```


Check IP:

```bash
ip a
```


Check routes:

```bash
ip route
```

---

# 🔌 Lab 10: Port Monitoring


Check listening ports:

```bash
ss -tulnp
```


Find SSH:

```bash
ss -tulnp | grep 22
```


Find HTTP:

```bash
ss -tulnp | grep 80
```

---

# 🌎 Lab 11: HTTP Testing


Using curl:

```bash
curl google.com
```


Check headers:

```bash
curl -I google.com
```

---

# 🔍 Lab 12: DNS Testing


Using nslookup:

```bash
nslookup google.com
```


Using dig:

```bash
dig google.com
```

---

# 📝 Troubleshooting Scenario


## Problem:

Unable to connect SSH server.


### Step 1: Check server reachable

```bash
ping server-ip
```


### Step 2: Check SSH service

```bash
systemctl status ssh
```


### Step 3: Check SSH port

```bash
ss -tulnp | grep 22
```


### Step 4: Debug SSH

```bash
ssh -v user@server
```

---

# 📸 Screenshot Checklist


Add your practical screenshots:

```text
screenshots/

├── ssh-service-status.png
├── ssh-key-generation.png
├── ssh-login-success.png
├── scp-transfer.png
├── rsync-sync.png
└── network-testing.png
```

---

# 📌 Commands Practiced


| Command | Purpose |
|-|-|
| ssh | Remote login |
| ssh-keygen | Generate SSH keys |
| ssh-copy-id | Copy public key |
| scp | Secure file copy |
| rsync | File synchronization |
| ping | Connectivity check |
| curl | HTTP testing |
| ss | Port checking |
| dig | DNS troubleshooting |


---

# 🎯 Real DevOps Usage


These skills are used for:

✔ AWS EC2 Administration  
✔ Server Access Management  
✔ Deployment Automation  
✔ Backup Automation  
✔ Network Debugging  
✔ Production Troubleshooting  


---

# 🚀 Lab Completed

Networking & SSH fundamentals successfully practiced for DevOps environments.
