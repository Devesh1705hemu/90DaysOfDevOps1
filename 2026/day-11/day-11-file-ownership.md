# Day 11 – File Ownership Challenge

## Objective
Learn how to:
- Understand file ownership in Linux
- Change file owners using `chown`
- Change groups using `chgrp`
- Apply recursive ownership changes
- Manage users and groups like a DevOps engineer

---

# Task 1: Understanding Ownership

## Check File Ownership

### Command
```bash
ls -l
```

### Example Output
```bash
-rw-r--r-- 1 user user 0 May 26 devops.txt
```

### Format Explanation
```text
-rw-r--r-- 1 owner group size date filename
```

| Section | Meaning |
|---|---|
| `-rw-r--r--` | File permissions |
| `1` | Link count |
| `owner` | File owner |
| `group` | File group |
| `size` | File size |
| `date` | Last modified |
| `filename` | File name |

---

## Difference Between Owner and Group

### Owner
- The main user who controls the file
- Usually has maximum permissions

### Group
- A collection of users
- Multiple users can access the file based on group permissions

---

# Task 2: Basic chown Operations

## Create File

```bash
touch devops-file.txt
```

---

## Check Current Owner

```bash
ls -l devops-file.txt
```

---

## Create Users

```bash
sudo useradd tokyo
sudo useradd berlin
```

---

## Change Owner to tokyo

```bash
sudo chown tokyo devops-file.txt
```

### Verify
```bash
ls -l devops-file.txt
```

---

## Change Owner to berlin

```bash
sudo chown berlin devops-file.txt
```

### Verify
```bash
ls -l devops-file.txt
```

---

# Task 3: Basic chgrp Operations

## Create File

```bash
touch team-notes.txt
```

---

## Check Current Group

```bash
ls -l team-notes.txt
```

---

## Create Group

```bash
sudo groupadd heist-team
```

---

## Change Group

```bash
sudo chgrp heist-team team-notes.txt
```

### Verify
```bash
ls -l team-notes.txt
```

---

# Task 4: Combined Owner & Group Change

## Create File

```bash
touch project-config.yaml
```

---

## Change Owner and Group Together

```bash
sudo chown professor:heist-team project-config.yaml
```

### Verify
```bash
ls -l project-config.yaml
```

---

## Create Directory

```bash
mkdir app-logs
```

---

## Change Directory Ownership

```bash
sudo chown berlin:heist-team app-logs
```

### Verify
```bash
ls -ld app-logs
```

---

# Task 5: Recursive Ownership

## Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

---

## Create Group

```bash
sudo groupadd planners
```

---

## Change Ownership Recursively

```bash
sudo chown -R professor:planners heist-project/
```

### Use
- `-R` applies ownership changes recursively
- Changes:
  - Parent directory
  - Subdirectories
  - Files inside directories

---

## Verify Recursive Changes

```bash
ls -lR heist-project/
```

---

# Task 6: Practice Challenge

## Create Users

```bash
sudo useradd tokyo
sudo useradd berlin
sudo useradd nairobi
```

---

## Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

---

## Create Directory

```bash
mkdir bank-heist
```

---

## Create Files

```bash
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

---

# Set Different Ownerships

## 1. access-codes.txt

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
```

---

## 2. blueprints.pdf

```bash
sudo chown berlin:tech-team bank-heist/blueprints.pdf
```

---

## 3. escape-plan.txt

```bash
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

---

## Verify Ownership

```bash
ls -l bank-heist/
```

### Example Output
```bash
-rw-r--r-- 1 tokyo   vault-team access-codes.txt
-rw-r--r-- 1 berlin  tech-team  blueprints.pdf
-rw-r--r-- 1 nairobi vault-team escape-plan.txt
```

---

# Key Commands Reference

## View Ownership

```bash
ls -l filename
```

### Use
Displays:
- Owner
- Group
- Permissions

---

## Change Owner Only

```bash
sudo chown newowner filename
```

### Example
```bash
sudo chown tokyo devops-file.txt
```

---

## Change Group Only

```bash
sudo chgrp newgroup filename
```

### Example
```bash
sudo chgrp heist-team team-notes.txt
```

---

## Change Owner and Group Together

```bash
sudo chown owner:group filename
```

### Example
```bash
sudo chown professor:heist-team project-config.yaml
```

---

## Recursive Ownership Change

```bash
sudo chown -R owner:group directory/
```

### Example
```bash
sudo chown -R professor:planners heist-project/
```

---

## Change Only Group Using chown

```bash
sudo chown :groupname filename
```

### Example
```bash
sudo chown :vault-team access-codes.txt
```

---

# Troubleshooting

## Permission Denied

### Solution
Use `sudo`

Example:
```bash
sudo chown tokyo file.txt
```

---

## Group Doesn't Exist

### Solution
Create group first

```bash
sudo groupadd groupname
```

---

## User Doesn't Exist

### Solution
Create user first

```bash
sudo useradd username
```

---

# Files & Directories Created

## Files
- devops-file.txt
- team-notes.txt
- project-config.yaml
- gold.txt
- strategy.conf
- access-codes.txt
- blueprints.pdf
- escape-plan.txt

---

## Directories
- app-logs/
- heist-project/
- heist-project/vault/
- heist-project/plans/
- bank-heist/

---

# Ownership Changes

| File | Ownership Change |
|---|---|
| devops-file.txt | user:user → tokyo |
| devops-file.txt | tokyo:user → berlin |
| team-notes.txt | user:user → user:heist-team |
| project-config.yaml | user:user → professor:heist-team |
| app-logs/ | user:user → berlin:heist-team |
| heist-project/ | user:user → professor:planners |
| access-codes.txt | user:user → tokyo:vault-team |
| blueprints.pdf | user:user → berlin:tech-team |
| escape-plan.txt | user:user → nairobi:vault-team |

---

# What I Learned

1. File ownership controls who manages files and directories.

2. Groups help multiple users share access securely.

3. Recursive ownership changes are important for managing entire projects efficiently.

---

# Why File Ownership Matters in DevOps

Proper ownership management is critical for:
- Application deployments
- Shared team environments
- CI/CD pipelines
- Container permissions
- Log management
- Server security

Incorrect ownership can break applications and create security risks.

---

# Commands Practiced

```bash
ls -l
chown
chgrp
useradd
groupadd
mkdir
touch
```

---


````
