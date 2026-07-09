# 🔑 SSH Key-Based Authentication

SSH Key-Based Authentication is a secure method used to access Linux servers without using passwords.

It is widely used by DevOps Engineers for managing cloud servers, automation tools, and production infrastructure.

---

## 📌 What is SSH Key Authentication?

SSH authentication uses a pair of cryptographic keys:

- Private Key
- Public Key


Instead of entering a password, SSH verifies the identity using these keys.

```
Local Machine
(Private Key)

        🔐 SSH Authentication

Remote Server
(Public Key)
```

---

# 🔐 Public Key vs Private Key


| Key | Description |
|-|-|
| Private Key | Stored securely on local machine |
| Public Key | Stored on remote server |
| Key Pair | Used together for authentication |


Important:

Never share your private key.

---

# ⚙️ Generate SSH Key Pair


Basic command:

```bash
ssh-keygen
```


Generate RSA 4096-bit key:

```bash
ssh-keygen -t rsa -b 4096
```


Generate with email:

```bash
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```


---

# 📂 SSH Key Location


Default location:

```bash
~/.ssh/
```


Files created:

```text
.ssh/

├── id_rsa
└── id_rsa.pub
```


Private key:

```bash
id_rsa
```


Public key:

```bash
id_rsa.pub
```


---

# 🔍 View Public Key


Command:

```bash
cat ~/.ssh/id_rsa.pub
```


Example:

```text
ssh-rsa AAAAB3NzaC1...
```


This key is copied to remote servers.

---

# 📤 Copy SSH Key to Server


Using ssh-copy-id:

```bash
ssh-copy-id user@server-ip
```


Example:

```bash
ssh-copy-id ubuntu@192.168.1.10
```


Now login:

```bash
ssh ubuntu@192.168.1.10
```


No password required.

---

# 🖥️ Manual Key Installation


Create SSH directory:

```bash
mkdir ~/.ssh
```


Create authorized keys file:

```bash
touch ~/.ssh/authorized_keys
```


Add public key:

```bash
nano ~/.ssh/authorized_keys
```


---

# 🔒 SSH File Permissions


Correct permissions are important.


SSH folder:

```bash
chmod 700 ~/.ssh
```


Private key:

```bash
chmod 600 ~/.ssh/id_rsa
```


Authorized keys:

```bash
chmod 600 ~/.ssh/authorized_keys
```


---

# ☁️ AWS EC2 SSH Authentication


AWS uses `.pem` private keys.


Set permission:

```bash
chmod 400 key.pem
```


Connect:

```bash
ssh -i key.pem ubuntu@public-ip
```


Example:

```bash
ssh -i devops.pem ubuntu@13.20.10.50
```


---

# ⚙️ SSH Config With Keys


Create config:

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


Connect easily:

```bash
ssh production
```


---

# 🧪 Practice Lab


## Task 1: Create SSH Key

```bash
ssh-keygen -t rsa -b 4096
```


---

## Task 2: Verify Keys

```bash
ls ~/.ssh
```


---

## Task 3: Copy Key

```bash
ssh-copy-id user@server
```


---

## Task 4: Login

```bash
ssh user@server
```


---

# 🛠️ Troubleshooting


## Permission Denied (publickey)


Fix permissions:

```bash
chmod 600 ~/.ssh/id_rsa
```


Check key:

```bash
ssh -i key.pem user@server
```


---

## Debug SSH Connection


Verbose mode:

```bash
ssh -v user@server
```


More details:

```bash
ssh -vvv user@server
```


---

# 📌 Command Summary


| Command | Usage |
|-|-|
| ssh-keygen | Generate keys |
| ssh-copy-id | Copy public key |
| ssh -i | Login with key |
| chmod 400 | Secure pem file |
| ssh -v | Debug SSH |
| cat id_rsa.pub | View public key |


---

# 🎯 DevOps Use Cases


SSH Keys are used for:

✔ AWS EC2 Access  
✔ GitHub Authentication  
✔ CI/CD Pipelines  
✔ Automated Deployments  
✔ Configuration Management Tools  


---

# 🚀 Skills Covered

- Secure Authentication
- SSH Key Management
- Linux Server Access
- Cloud Server Management
- DevOps Security Practices
