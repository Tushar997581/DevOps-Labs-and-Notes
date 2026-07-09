# 📄 Linux Text Processing for DevOps Engineers

Text processing is an essential Linux skill used by DevOps Engineers for analyzing logs, filtering data, debugging issues, and automating tasks.

Linux provides powerful command-line tools to process large amounts of text efficiently.

---

# 📌 Why Text Processing Matters?

In production environments, engineers work with:

- Application logs
- Server logs
- Configuration files
- Monitoring outputs
- Deployment reports

Text processing helps quickly find useful information.

---

# 🔍 grep Command

`grep` is used to search patterns inside files.

Syntax:

```bash
grep "pattern" filename
```

Example:

```bash
grep "ERROR" application.log
```

---

## Ignore Case

```bash
grep -i "error" application.log
```

---

## Search Recursively

Search inside directories:

```bash
grep -r "failed" /var/log/
```

---

## Show Line Numbers

```bash
grep -n "error" file.txt
```

---

## Count Matches

```bash
grep -c "error" file.txt
```

---

# ✂️ cut Command

`cut` extracts specific sections from text.

---

## Extract Columns

Example file:

```text
john:admin:1001
alex:user:1002
```

Command:

```bash
cut -d ":" -f1 users.txt
```

Output:

```text
john
alex
```

---

# 📊 awk Command

`awk` is a powerful text processing language.

Used for:

- Extracting columns
- Formatting output
- Processing logs


---

## Print Columns

Example:

```bash
awk '{print $1}' file.txt
```

Print multiple columns:

```bash
awk '{print $1,$3}' file.txt
```

---

## Filter Data


Example:

```bash
awk '$3 > 80 {print $0}' cpu.txt
```

Shows records where column 3 is greater than 80.

---

# 🔄 sed Command

`sed` is a stream editor used to modify text.

Common uses:

- Replace text
- Delete lines
- Edit configuration files

---

## Replace Text


Syntax:

```bash
sed 's/old/new/' file.txt
```

Example:

```bash
sed 's/dev/test/' config.txt
```

---

## Replace Globally


```bash
sed 's/error/ERROR/g' logs.txt
```

---

## Delete Lines


Delete first line:

```bash
sed '1d' file.txt
```

---

# 🔃 sort Command


Sort file content:

```bash
sort names.txt
```


Reverse sorting:

```bash
sort -r names.txt
```


Numeric sorting:

```bash
sort -n numbers.txt
```

---

# 🧹 uniq Command


Remove duplicate lines:

```bash
uniq file.txt
```


Count duplicates:

```bash
uniq -c file.txt
```


Usually used with sort:

```bash
sort file.txt | uniq
```

---

# 🔗 Pipes in Linux


Pipe sends output of one command to another.


Example:

```bash
cat app.log | grep ERROR
```


Multiple commands:

```bash
cat access.log | grep 404 | wc -l
```

---

# 📈 wc Command


Count lines:

```bash
wc -l file.txt
```


Count words:

```bash
wc -w file.txt
```


Count characters:

```bash
wc -c file.txt
```

---

# 🧪 DevOps Log Analysis Examples


## Find Application Errors

```bash
grep ERROR application.log
```

---

## Count Failed Login Attempts

```bash
grep "Failed password" /var/log/auth.log | wc -l
```

---

## Find Top IP Addresses

```bash
awk '{print $1}' access.log | sort | uniq -c
```

---

## Monitor Live Logs

```bash
tail -f application.log | grep ERROR
```

---

# 📌 Command Summary


| Command | Purpose |
|-|-|
| grep | Search text |
| awk | Process columns |
| sed | Modify text |
| cut | Extract fields |
| sort | Sort data |
| uniq | Remove duplicates |
| wc | Count output |
| pipe `|` | Combine commands |


---

# 🎯 DevOps Use Cases


Text processing helps with:

✔ Log analysis  
✔ Debugging production issues  
✔ Monitoring servers  
✔ Creating automation scripts  
✔ Processing CI/CD outputs  
✔ Configuration management  


---

# 🚀 Skills Covered

- grep
- awk
- sed
- Linux Pipelines
- Log Analysis
- Automation
- DevOps Troubleshooting
