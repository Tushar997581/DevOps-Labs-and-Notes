# 📂 Secure File Transfer in Linux (SCP & Rsync)

File transfer is an important part of Linux Administration and DevOps workflows.

DevOps Engineers frequently transfer configuration files, application builds, backups, and logs between local machines and remote servers.

---

## 📌 File Transfer Methods

Common Linux file transfer tools:

- SCP (Secure Copy Protocol)
- Rsync (Remote Synchronization)

Both tools use SSH for secure encrypted communication.

---

# 🔐 SCP (Secure Copy Protocol)

SCP securely copies files between systems using SSH.

Syntax:

```bash
scp source destination
```

---

# 📤 Copy File From Local to Remote Server


Command:

```bash
scp file.txt user@server-ip:/home/user/
```


Example:

```bash
scp app.log ubuntu@192.168.1.20:/home/ubuntu/
```


Flow:

```
Local Machine
      |
      | SCP
      |
Remote Server
```

---

# 📥 Copy File From Remote to Local


Command:

```bash
scp user@server-ip:/path/file .
```


Example:

```bash
scp ubuntu@192.168.1.20:/var/log/app.log .
```

---

# 📁 Copy Directory Using SCP


Use `-r` option:

```bash
scp -r project/ user@server:/home/user/
```


Example:

```bash
scp -r website/ ubuntu@server:/var/www/html/
```

---

# 🔑 SCP Using SSH Key


AWS EC2 example:

```bash
scp -i key.pem file.txt ubuntu@public-ip:/home/ubuntu/
```


---

# 🚀 Rsync (Remote Synchronization)


Rsync is a powerful file synchronization tool.

It transfers only changed data, making it faster than SCP.


Advantages:

✔ Faster transfers  
✔ Supports incremental sync  
✔ Good for backups  
✔ Preserves permissions  


---

# 📤 Sync Local Directory to Server


Command:

```bash
rsync -av folder/ user@server:/backup/
```


Example:

```bash
rsync -av project/ ubuntu@192.168.1.20:/home/ubuntu/project/
```

---

# 📥 Sync Remote Directory Locally


Command:

```bash
rsync -av user@server:/backup/ ./backup/
```

Example:

```bash
rsync -av ubuntu@server:/var/log/ ./logs/
```

---

# 🔑 Rsync With SSH Key


Command:

```bash
rsync -av -e "ssh -i key.pem" folder/ ubuntu@server:/backup/
```

---

# 🗑️ Delete Removed Files During Sync


Make destination exactly same as source:

```bash
rsync -av --delete source/ destination/
```

---

# 📊 Show Transfer Progress


Command:

```bash
rsync -av --progress file user@server:/path/
```

---

# ⚙️ Common Rsync Options


| Option | Usage |
|-|-|
| -a | Archive mode |
| -v | Verbose output |
| -z | Compress data |
| -r | Recursive copy |
| --delete | Remove deleted files |
| --progress | Show progress |


---

# 🧪 Practical DevOps Example


## Backup Application Logs


Create backup folder:

```bash
mkdir backup
```


Copy logs:

```bash
rsync -av /var/log/nginx/ backup/
```


Transfer backup:

```bash
rsync -av backup/ ubuntu@server:/backup/
```

---

# 🔄 Deployment Example


Transfer website files:

```bash
rsync -av build/ ubuntu@server:/var/www/html/
```


Restart service:

```bash
ssh ubuntu@server "sudo systemctl restart nginx"
```

---

# 🔎 Troubleshooting


## Permission Denied


Check SSH:

```bash
ssh user@server
```


Check file permissions:

```bash
ls -l
```


---

## Connection Problem


Test network:

```bash
ping server-ip
```


Check SSH port:

```bash
ss -tulnp | grep ssh
```

---

# 📌 SCP vs Rsync


| Feature | SCP | Rsync |
|-|-|-|
| SSH Based | ✅ | ✅ |
| Simple Copy | ✅ | ✅ |
| Incremental Sync | ❌ | ✅ |
| Backup Friendly | ❌ | ✅ |
| Faster Large Transfer | ❌ | ✅ |


---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| scp file server:path | Copy file |
| scp -r | Copy directory |
| rsync -av | Sync files |
| rsync --delete | Mirror folders |
| rsync --progress | Show progress |


---

# 🎯 DevOps Use Cases


File transfer skills help with:

✔ Application deployment  
✔ Server migration  
✔ Backup automation  
✔ Log collection  
✔ Cloud server management  


---

# 🚀 Skills Covered

- Secure File Transfer
- SCP
- Rsync
- Backup Management
- Linux Server Operations
- DevOps Automation
