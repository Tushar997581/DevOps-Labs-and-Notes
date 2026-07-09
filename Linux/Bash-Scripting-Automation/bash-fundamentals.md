# 🐚 Bash Fundamentals for DevOps Engineers

Bash (Bourne Again Shell) is a command-line interpreter used to interact with Linux systems.

DevOps Engineers use Bash scripts to automate server tasks, deployments, monitoring, and daily operations.

---

# 📌 What is Bash?

Bash allows users to:

- Execute Linux commands
- Create automation scripts
- Manage servers
- Process files
- Automate repetitive tasks


Examples:

- Backup automation
- Log cleanup
- Health checks
- Deployment scripts

---

# 📝 Creating First Bash Script


Create a file:

```bash
touch hello.sh
```


Open file:

```bash
nano hello.sh
```


Add:

```bash
#!/bin/bash

echo "Hello DevOps"
```


Run script:

```bash
bash hello.sh
```

---

# 🚀 Make Script Executable


Add execute permission:

```bash
chmod +x hello.sh
```


Run:

```bash
./hello.sh
```

---

# 🔹 Shebang (#!)


First line of script:

```bash
#!/bin/bash
```


Purpose:

- Defines script interpreter
- Tells Linux to use Bash shell

---

# 📦 Bash Variables


Variables store values.

Example:

```bash
#!/bin/bash

tool="Docker"

echo "Learning $tool"
```


Output:

```text
Learning Docker
```

---

# 🌍 Environment Variables


View environment variables:

```bash
env
```


Common variables:

```bash
$HOME

$USER

$PATH
```


Example:

```bash
echo $HOME
```

---

# ⌨️ User Input


Take input from user:

```bash
#!/bin/bash

echo "Enter your name:"

read name

echo "Welcome $name"
```

---

# 🎯 Script Arguments


Arguments are values passed while running scripts.


Script:

```bash
#!/bin/bash

echo "First argument: $1"

echo "Second argument: $2"
```


Run:

```bash
./script.sh Linux DevOps
```


Output:

```text
First argument: Linux

Second argument: DevOps
```

---

# 🔢 Special Variables


| Variable | Meaning |
|-|-|
| $0 | Script name |
| $1-$9 | Arguments |
| $# | Number of arguments |
| $? | Exit status |
| $$ | Process ID |


---

# ✔️ Exit Status


Check previous command result:

```bash
echo $?
```


Meaning:

```text
0 = Success

Non-zero = Error
```

Example:

```bash
mkdir test

echo $?
```

---

# 🔀 Conditional Statements


## if Statement


Example:

```bash
#!/bin/bash


if [ -f file.txt ]

then

echo "File exists"

else

echo "File not found"

fi
```

---

# 🔁 Loops


## For Loop


Example:

```bash
#!/bin/bash


for i in 1 2 3 4 5

do

echo $i

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


Functions reuse code.


Example:

```bash
#!/bin/bash


server_status(){

echo "Checking Server"

uptime

}


server_status
```

---

# 📂 File Testing Operators


| Operator | Meaning |
|-|-|
| -f | File exists |
| -d | Directory exists |
| -r | Read permission |
| -w | Write permission |
| -x | Execute permission |


Example:

```bash
if [ -d /var/log ]

then

echo "Directory exists"

fi
```

---

# 🧪 Practice Tasks


## Task 1: Create Script

```bash
touch devops.sh

chmod +x devops.sh
```


---

## Task 2: Print System Info


```bash
#!/bin/bash

hostname

uptime

free -h
```


---

## Task 3: Use Arguments


```bash
#!/bin/bash

echo "Deploying $1"
```


Run:

```bash
./deploy.sh nginx
```

---

# 📌 Commands Summary


| Command | Usage |
|-|-|
| bash script.sh | Run script |
| chmod +x | Add execute permission |
| echo | Print output |
| read | User input |
| env | Environment variables |
| $? | Exit status |


---

# 🎯 DevOps Use Cases


Bash fundamentals help with:

✔ Deployment automation  
✔ Server health checks  
✔ Backup scripts  
✔ CI/CD pipelines  
✔ Log processing  
✔ Cloud automation  


---

# 🚀 Skills Covered

- Bash Shell
- Linux Automation
- Variables
- Conditions
- Loops
- Functions
- DevOps Scripting
