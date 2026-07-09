# 🌍 Environment Variables for DevOps Engineers

Environment variables are dynamic values used by operating systems, applications, containers, and automation tools to manage configuration.

They allow applications to run in different environments without changing source code.

---

# 📌 What are Environment Variables?

Environment variables store:

- Application settings
- System paths
- Configuration values
- Credentials references
- Runtime information

Examples:

- Development environment
- Production environment
- Database configuration
- API configuration

---

# 🔎 View Environment Variables

Show all variables:

```bash
env
```

or

```bash
printenv
```

---

# 🔍 View Specific Variable

Example:

```bash
echo $HOME
```

```bash
echo $USER
```

```bash
echo $PATH
```

---

# 📌 Common Linux Variables


| Variable | Purpose |
|-|-|
| HOME | User home directory |
| USER | Current username |
| PATH | Executable command paths |
| SHELL | Current shell |
| PWD | Current directory |
| HOSTNAME | System hostname |

---

# ➕ Create Temporary Environment Variable

Temporary variables exist only for the current terminal session.


Example:

```bash
export APP_ENV=production
```

Check:

```bash
echo $APP_ENV
```

Output:

```text
production
```

---

# ❌ Remove Environment Variable


Command:

```bash
unset APP_ENV
```

Verify:

```bash
echo $APP_ENV
```

---

# 📂 Permanent Environment Variables


To save variables permanently add them into shell configuration files.

---

## ~/.bashrc


Open:

```bash
nano ~/.bashrc
```


Add:

```bash
export APP_ENV=production
export APP_PORT=8080
```


Reload:

```bash
source ~/.bashrc
```

---

# 🧾 ~/.profile


Used during login shell sessions.


Edit:

```bash
nano ~/.profile
```


Add:

```bash
export JAVA_HOME=/usr/bin/java
```

---

# 🌐 System Wide Environment Variables


Available for all users.


File:

```bash
/etc/environment
```


Edit:

```bash
sudo nano /etc/environment
```


Example:

```bash
APP_ENV="production"
```

---

# 📦 .env Files


Applications commonly store configuration inside `.env` files.


Example:

```env
APP_ENV=production

APP_PORT=5000

DATABASE_HOST=db.example.com

DATABASE_PORT=3306
```

---

# 🐳 Docker Environment Variables


Pass variable:

```bash
docker run \
-e APP_ENV=production \
nginx
```

---

# Docker Compose Example


```yaml
services:

  app:

    image: nginx

    environment:

      APP_ENV: production
```

---

# ☸️ Kubernetes Environment Variables


Pod example:

```yaml
containers:

- name: app

  image: nginx

  env:

  - name: APP_ENV

    value: production
```

---

# ⚙️ CI/CD Environment Variables


Used in:

- GitHub Actions
- Jenkins
- GitLab CI


Example GitHub Actions:

```yaml
env:

  APP_ENV: production
```

---

# 🔐 Secrets vs Environment Variables


Environment Variables:

```text
APP_MODE=production
```

Secrets:

```text
DATABASE_PASSWORD
API_KEYS
TOKENS
```

Sensitive values should be stored in secret managers.

---

# 🧪 Practice Lab


Create variable:

```bash
export PROJECT=DevOps
```


Check:

```bash
echo $PROJECT
```


Add permanently:

```bash
echo "export PROJECT=DevOps" >> ~/.bashrc
```


Reload:

```bash
source ~/.bashrc
```

---

# 🔥 Troubleshooting


## Variable Not Found


Check:

```bash
echo $VARIABLE_NAME
```


Reload config:

```bash
source ~/.bashrc
```


---

## PATH Issue


View:

```bash
echo $PATH
```


Add path:

```bash
export PATH=$PATH:/new/path
```

---

# 📌 Command Summary


| Command | Usage |
|-|-|
| env | Show variables |
| printenv | Display environment |
| export | Create variable |
| unset | Remove variable |
| source | Reload config |
| echo $VAR | Print value |


---

# 🎯 DevOps Use Cases


Environment variables are used in:

✔ Application configuration  
✔ Docker containers  
✔ Kubernetes deployments  
✔ CI/CD pipelines  
✔ Cloud automation  
✔ Secure configuration management  


---

# 🚀 Skills Covered

- Linux Environment Management
- Application Configuration
- Docker ENV
- Kubernetes ENV
- CI/CD Configuration
- Production Operations
