# Day 10 – Linux File Permissions & File Access

## Objective
Learn how to:
- Create and read files
- Understand Linux permissions
- Modify file permissions
- Test permission behavior
- Practice real Linux commands used in DevOps

---

# Task 1: Create Files

## 1. Create an Empty File

### Command
```bash
touch devops.txt
```

### Use
Creates an empty file quickly.

---

## 2. Create `notes.txt` with Content

### Using `echo`

```bash
echo "Linux permissions are important in DevOps" > notes.txt
```

### Use
Writes content into the file.

---

### OR Using `cat`

```bash
cat > notes.txt
```

Type:

```text
Linux permissions are important in DevOps
```

Press:

```text
CTRL + D
```

### Use
Creates file and accepts user input from terminal.

---

## 3. Create `script.sh` Using Vim

### Command
```bash
vim script.sh
```

Press:

```text
i
```

Add:

```bash
echo "Hello DevOps"
```

Save and Exit:

```text
ESC
:wq
```

### Use
Creates and edits shell scripts.

---

## 4. Verify Files and Permissions

### Command
```bash
ls -l
```

### Example Output
```bash
-rw-r--r-- 1 user user   0 May 26 10:00 devops.txt
-rw-r--r-- 1 user user  40 May 26 10:01 notes.txt
-rw-r--r-- 1 user user  20 May 26 10:02 script.sh
```

### Use
Displays:
- File permissions
- Owner
- Size
- Date
- File name

---

# Task 2: Read Files

## 1. Read `notes.txt`

### Command
```bash
cat notes.txt
```

### Use
Displays file content.

---

## 2. Open `script.sh` in Read-Only Mode

### Command
```bash
vim -R script.sh
```

### Use
Opens file without allowing modification.

---

## 3. Display First 5 Lines of `/etc/passwd`

### Command
```bash
head -5 /etc/passwd
```

### Use
Displays first lines of a file.

---

## 4. Display Last 5 Lines of `/etc/passwd`

### Command
```bash
tail -5 /etc/passwd
```

### Use
Displays last lines of a file.

---

# Task 3: Understand Permissions

## Permission Format

```text
rwxrwxrwx
```

Split into:

```text
rwx | rwx | rwx
Owner Group Others
```

---

## Permission Values

| Permission | Meaning | Value |
|---|---|---|
| r | Read | 4 |
| w | Write | 2 |
| x | Execute | 1 |

---

## Check File Permissions

### Command
```bash
ls -l devops.txt notes.txt script.sh
```

### Example Output
```bash
-rw-r--r--  devops.txt
-rw-r--r--  notes.txt
-rw-r--r--  script.sh
```

---

## Permission Explanation

### Owner Permissions

```text
rw-
```

Owner Can:
- Read
- Write
- Cannot execute

---

### Group Permissions

```text
r--
```

Group Can:
- Read only

---

### Others Permissions

```text
r--
```

Others Can:
- Read only

---

# Task 4: Modify Permissions

## 1. Make `script.sh` Executable

### Command
```bash
chmod +x script.sh
```

### Check Permissions
```bash
ls -l script.sh
```

### Example Output
```bash
-rwxr-xr-x
```

### Run Script
```bash
./script.sh
```

### Output
```text
Hello DevOps
```

### Use
Adds execute permission to the script.

---

## 2. Set `devops.txt` to Read-Only

### Command
```bash
chmod a-w devops.txt
```

### Verify
```bash
ls -l devops.txt
```

### Example Output
```bash
-r--r--r--
```

### Use
Removes write permission for everyone.

---

## 3. Set `notes.txt` Permission to `640`

### Command
```bash
chmod 640 notes.txt
```

### Verify
```bash
ls -l notes.txt
```

### Example Output
```bash
-rw-r-----
```

### Meaning
- Owner → Read + Write
- Group → Read only
- Others → No permission

---

## 4. Create `project` Directory with `755` Permission

### Create Directory
```bash
mkdir project
```

### Set Permission
```bash
chmod 755 project
```

### Verify
```bash
ls -ld project
```

### Example Output
```bash
drwxr-xr-x
```

### Meaning
- Owner → Full access
- Group → Read + Execute
- Others → Read + Execute

---

# Task 5: Test Permissions

## 1. Try Writing to Read-Only File

### Command
```bash
echo "test" >> devops.txt
```

### Error
```text
Permission denied
```

### Reason
Write permission was removed.

---

## 2. Try Executing File Without Execute Permission

### Remove Execute Permission
```bash
chmod -x script.sh
```

### Run Script
```bash
./script.sh
```

### Error
```text
Permission denied
```

### Reason
Execute permission is missing.

---

# Important Permission Numbers

| Number | Permission |
|---|---|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 0 | --- |

---

# Common Permission Examples

| Command | Meaning |
|---|---|
| `chmod 777 file` | Full access to everyone |
| `chmod 755 file` | Owner full access, others read & execute |
| `chmod 644 file` | Owner read/write, others read only |
| `chmod 600 file` | Only owner can access |

---

# Commands Practiced

| Command | Use |
|---|---|
| `touch` | Create empty files |
| `echo` | Print or write text |
| `cat` | Display file content |
| `vim` | Edit files |
| `ls -l` | View permissions and file details |
| `head` | View first lines |
| `tail` | View last lines |
| `chmod` | Change permissions |
| `mkdir` | Create directories |
| `./script.sh` | Execute script |

---

# Real DevOps Learning

Linux permissions are critical in DevOps because they help:
- Secure scripts and files
- Prevent unauthorized access
- Control execution rights
- Protect production servers
- Troubleshoot permission issues quickly
