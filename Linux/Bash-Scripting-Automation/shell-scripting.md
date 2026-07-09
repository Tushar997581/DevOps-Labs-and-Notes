# 🐚 Shell Scripting for DevOps Engineers

Shell scripting is a powerful way to automate Linux tasks and build repeatable workflows.

DevOps Engineers use shell scripts for deployments, monitoring, backups, server configuration, and CI/CD automation.

---

# 📌 What is Shell Scripting?

A shell script is a file containing multiple Linux commands executed together.

Shell scripts help:

- Reduce manual work
- Automate repeated tasks
- Improve consistency
- Save time
- Reduce human errors

---

# 📝 Basic Script Structure


Create script:

```bash
touch script.sh
```


Open:

```bash
nano script.sh
```


Example:

```bash
#!/bin/bash

echo "Starting DevOps Automation"

date

uptime
```


Run:

```bash
bash script.sh
```

---

# 🚀 Script Permission


Make executable:

```bash
chmod +x script.sh
```


Execute:

```bash
./script.sh
```

---

# 📦 Variables


Variables store data values.


Example:

```bash
#!/bin/bash

app="nginx"

echo "Deploying $app"
```

---

# 🌍 Environment Variables


Print variables:

```bash
echo $USER

echo $HOME

echo $PATH
```


Create variable:

```bash
export ENV="production"
```

---

# ⌨️ User Input


Read command:

```bash
#!/bin/bash

echo "Enter service name"

read service

systemctl status $service
```

---

# 🎯 Script Arguments


Script:

```bash
#!/bin/bash

echo "Application: $1"

echo "Version: $2"
```


Run:

```bash
./deploy.sh nginx v1
```


Output:

```text
Application: nginx

Version: v1
```

---

# 🔀 Conditional Statements


## If Else


Example:

```bash
#!/bin/bash


if [ -f app.log ]

then

echo "Log file exists"

else

echo "File missing"

fi
```

---

# 🔎 Check Service Status Script


Example:

```bash
#!/bin/bash


service="nginx"


if systemctl is-active --quiet $service

then

echo "$service running"

else

echo "$service stopped"

fi
```

---

# 🔁 Loops


## For Loop


Example:

```bash
#!/bin/bash


for server in web1 web2 web3

do

echo "Checking $server"

done
```

---

## While Loop


Example:

```bash
#!/bin/bash


count=1


while [ $count -le 5 ]

do

echo $count

((count++))

done
```

---

# 🧩 Functions


Functions allow reusable code.


Example:

```bash
#!/bin/bash


check_disk(){

df -h

}


check_disk
```

---

# 📂 File Operations


Create file:

```bash
touch test.txt
```


Check file:

```bash
if [ -f test.txt ]

then

echo "Available"

fi
```

---

# 🔥 Error Handling


Exit status:

```bash
echo $?
```


Example:

```bash
#!/bin/bash


mkdir backup


if [ $? -eq 0 ]

then

echo "Success"

else

echo "Failed"

fi
```

---

# 📜 Case Statement


Example:

```bash
#!/bin/bash


echo "start | stop"

read action


case $action in

start)

echo "Starting service"

;;


stop)

echo "Stopping service"

;;


*)

echo "Invalid option"

;;

esac
```

---

# 🧪 DevOps Automation Examples


# Server Health Script


```bash
#!/bin/bash


echo "CPU Info"

uptime


echo "Memory"

free -h


echo "Disk"

df -h
```

---

# Backup Script


```bash
#!/bin/bash


DATE=$(date +%F)


tar -czf backup-$DATE.tar.gz /var/log
```

---

# Log Checker


```bash
#!/bin/bash


grep ERROR /var/log/syslog
```

---

# 📌 Script Debugging


Run script debugging mode:

```bash
bash -x script.sh
```

---

# 📌 Operators


| Operator | Meaning |
|-|-|
| -eq | Equal |
| -ne | Not equal |
| -gt | Greater than |
| -lt | Less than |
| -f | File exists |
| -d | Directory exists |


---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| chmod +x | Execute permission |
| read | User input |
| if else | Decision making |
| for | Loop execution |
| while | Conditional loop |
| function | Reusable block |
| case | Multiple choices |
| bash -x | Debug script |


---

# 🎯 DevOps Use Cases


Shell scripting is used for:

✔ Deployment automation  
✔ Backup management  
✔ Log monitoring  
✔ Health checks  
✔ CI/CD pipelines  
✔ Infrastructure tasks  


---

# 🚀 Skills Covered

- Shell Automation
- Variables
- Conditions
- Loops
- Functions
- Error Handling
- DevOps Scripting
