# 🌐 Networking & SSH for DevOps Engineers

Networking and SSH are essential skills for managing cloud servers, remote infrastructure, and production environments.

This section covers secure remote access, server communication, file transfer, and network troubleshooting concepts used by DevOps Engineers.

---

## 📌 Topics Covered

### 🔐 SSH (Secure Shell)

SSH allows secure remote access to Linux servers.

Concepts:

- Remote server login
- SSH client & server
- Secure communication
- Authentication methods
- SSH configuration

Common command:

```bash
ssh username@server-ip
```

Example:

```bash
ssh ubuntu@192.168.1.10
```

---

# 🔑 SSH Key-Based Authentication

SSH keys provide secure passwordless authentication.

Key components:

- Public Key
- Private Key


Generate SSH key:

```bash
ssh-keygen
```


Generate RSA 4096-bit key:

```bash
ssh-keygen -t rsa -b 4096
```


Copy public key to server:

```bash
ssh-copy-id user@server-ip
```

Benefits:

✔ More secure than passwords  
✔ Required for cloud servers  
✔ Used in automation tools  

---

# ⚙️ SSH Configuration

SSH config simplifies server connections.

Configuration file:

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


Now connect using:

```bash
ssh production
```

---

# 📂 File Transfer Between Servers


## SCP (Secure Copy)

Copy local file to server:

```bash
scp file.txt user@server:/home/user/
```


Copy from server:

```bash
scp user@server:/home/user/file.txt .
```


---

## Rsync

Efficient file synchronization:

```bash
rsync -av folder/ user@server:/backup/
```

Advantages:

- Faster transfers
- Sync only changes
- Useful for backups


---

# 🌍 Networking Commands


## Check Connectivity

```bash
ping google.com
```


---

## Test URLs/APIs

```bash
curl https://example.com
```


---

## Check Open Ports

```bash
ss -tulnp
```


or:

```bash
netstat -tulnp
```


---

## DNS Lookup

```bash
nslookup google.com
```


or

```bash
dig google.com
```


---

# 🧪 Hands-on Practice

Practical tasks:

✔ Create SSH keys  
✔ Configure passwordless login  
✔ Connect remote Linux servers  
✔ Transfer files using SCP  
✔ Synchronize files using Rsync  
✔ Debug network connectivity  


---

# 🛠️ Tools Used

- OpenSSH
- Linux Terminal
- SCP
- Rsync
- Curl
- Netstat / SS


---

# 🎯 DevOps Use Cases

Networking & SSH skills help with:

✔ Managing AWS EC2 instances  
✔ Connecting production servers  
✔ Automating deployments  
✔ CI/CD server access  
✔ Troubleshooting network issues  


---

# 🚀 Skills Covered

- Linux Networking
- SSH Administration
- Secure Authentication
- Server Management
- Network Troubleshooting
- DevOps Operations


---

# 📚 Part of DevOps Engineer Handbook

Learning Path:

Linux Administration → Networking & SSH → Bash Automation → Docker → Kubernetes → Cloud → CI/CD
