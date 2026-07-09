# 🐚 Bash Scripting & Automation for DevOps Engineers

Bash scripting is one of the most important skills for DevOps Engineers to automate repetitive tasks, manage servers, and build efficient workflows.

This section covers Linux shell scripting, text processing, automation scripts, and real-world DevOps use cases.

---

## 📌 Topics Covered


## 🔹 Bash Fundamentals

Understanding Linux shell and scripting basics.

Concepts:

- Bash Shell
- Shell Scripts
- Variables
- User Input
- Arguments
- Exit Status
- Permissions


Create a shell script:

```bash
touch script.sh
```


Add executable permission:

```bash
chmod +x script.sh
```


Run script:

```bash
./script.sh
```


---

# 🔹 Variables in Bash


Example:

```bash
#!/bin/bash

name="DevOps"

echo "Learning $name"
```


Output:

```text
Learning DevOps
```

---

# 🔹 User Input


Read input from user:

```bash
#!/bin/bash

echo "Tushar:"

read name

echo "Hello $name"
```

---

# 🔹 Conditional Statements


If condition:

```bash
#!/bin/bash

if [ -f file.txt ]

then

echo "File exists"

else

echo "File missing"

fi
```

---

# 🔹 Loops


For loop:

```bash
for i in {1..5}

do

echo $i

done
```


While loop:

```bash
count=1

while [ $count -le 5 ]

do

echo $count

((count++))

done
```

---

# 📄 Text Processing


Linux provides powerful tools to process files and logs.


## grep

Search text:

```bash
grep "error" app.log
```


---

## awk

Extract columns:

```bash
awk '{print $1}' file.txt
```


---

## sed

Replace text:

```bash
sed 's/old/new/g' file.txt
```


---

## sort

Sort output:

```bash
sort file.txt
```


---

## uniq

Remove duplicates:

```bash
uniq file.txt
```


---

# ⚙️ Automation Examples


## Backup Script

```bash
#!/bin/bash

tar -czf backup.tar.gz /var/log
```


---

## Server Health Check

```bash
#!/bin/bash

df -h

free -h

uptime
```


---

## Log Monitoring

```bash
#!/bin/bash

grep ERROR /var/log/syslog
```

---

# 🧪 Hands-on Practice

Practical tasks:

✔ Create shell scripts  
✔ Automate Linux commands  
✔ Analyze logs  
✔ Create backup scripts  
✔ Monitor system resources  
✔ Execute scheduled tasks  


---

# 🛠️ Tools Used

- Bash Shell
- Linux Terminal
- grep
- awk
- sed
- cron
- Shell Scripts


---

# 🎯 DevOps Use Cases


Bash scripting helps with:

✔ Server automation  
✔ CI/CD workflows  
✔ Log analysis  
✔ Backup automation  
✔ Infrastructure management  
✔ Production operations  


---

# 🚀 Skills Covered

- Shell Scripting
- Linux Automation
- Text Processing
- Server Management
- DevOps Operations


---

# 📚 Part of DevOps Engineer Handbook


Learning Path:

Linux Administration → Networking & SSH → Bash Automation → Docker → Kubernetes → Cloud → CI/CD
