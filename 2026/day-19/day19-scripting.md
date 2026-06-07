# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## Objective

Apply shell scripting concepts to automate common system administration tasks:

* Log Rotation
* Server Backup
* Cron Scheduling
* Scheduled Maintenance

---

# Task 1: Log Rotation Script

## Script: `log_rotate.sh`

```bash
#!/bin/bash

if [ $# -ne 1 ]; then
    echo "Usage: $0 <log_directory>"
    exit 1
fi

log_dir="$1"

if [ ! -d "$log_dir" ]; then
    echo "Error: Directory does not exist."
    exit 1
fi

compressed_count=$(find "$log_dir" -type f -name "*.log" -mtime +7 | wc -l)

find "$log_dir" -type f -name "*.log" -mtime +7 -exec gzip {} \;

deleted_count=$(find "$log_dir" -type f -name "*.gz" -mtime +30 | wc -l)

find "$log_dir" -type f -name "*.gz" -mtime +30 -delete

echo "Compressed files: $compressed_count"
echo "Deleted files: $deleted_count"
```

### Sample Output

```text
Compressed files: 3
Deleted files: 1
```

---

# Task 2: Server Backup Script

## Script: `backup.sh`

```bash
#!/bin/bash

if [ $# -ne 2 ]; then
    echo "Usage: $0 <source_directory> <backup_directory>"
    exit 1
fi

source_dir="$1"
backup_dir="$2"

if [ ! -d "$source_dir" ]; then
    echo "Error: Source directory does not exist."
    exit 1
fi

mkdir -p "$backup_dir"

timestamp=$(date +%Y-%m-%d)

archive_name="backup-${timestamp}.tar.gz"
archive_path="${backup_dir}/${archive_name}"

tar -czf "$archive_path" "$source_dir"

if [ $? -ne 0 ] || [ ! -f "$archive_path" ]; then
    echo "Error: Failed to create backup archive."
    exit 1
fi

archive_size=$(du -h "$archive_path" | cut -f1)

deleted_count=$(find "$backup_dir" -type f -name "backup-*.tar.gz" -mtime +14 | wc -l)

find "$backup_dir" -type f -name "backup-*.tar.gz" -mtime +14 -delete

echo "Backup created successfully!"
echo "Archive Name: $archive_name"
echo "Archive Size: $archive_size"
echo "Old Backups Deleted: $deleted_count"
```

### Sample Output

```text
Backup created successfully!
Archive Name: backup-2026-06-07.tar.gz
Archive Size: 4.0K
Old Backups Deleted: 0
```

---

# Task 3: Crontab

## Check Existing Scheduled Jobs

```bash
crontab -l
```

## Cron Entries

### Run log_rotate.sh every day at 2:00 AM

```cron
0 2 * * * /home/ubuntu/day19-scripting/task1/log_rotate.sh /var/log/myapp
```

### Run backup.sh every Sunday at 3:00 AM

```cron
0 3 * * 0 /home/ubuntu/day19-scripting/task2/backup.sh /home/ubuntu/hiest-project /home/ubuntu/backups
```

### Run health_check.sh every 5 minutes

```cron
*/5 * * * * /home/ubuntu/scripts/health_check.sh
```

---

# Task 4: Scheduled Maintenance Script

## Script: `maintenance.sh`

```bash
#!/bin/bash

log_file="$HOME/maintenance.log"

echo "====================================" >> "$log_file"
echo "Maintenance Started: $(date)" >> "$log_file"

echo "Running Log Rotation..." >> "$log_file"
/home/ubuntu/day19-scripting/task1/log_rotate.sh /var/log/myapp >> "$log_file" 2>&1

echo "Running Backup..." >> "$log_file"
/home/ubuntu/day19-scripting/task2/backup.sh /home/ubuntu/hiest-project /home/ubuntu/backups >> "$log_file" 2>&1

echo "Maintenance Completed: $(date)" >> "$log_file"
echo "====================================" >> "$log_file"
echo "" >> "$log_file"
```

### Sample Output (maintenance.log)

```text
====================================
Maintenance Started: Sat Jun 07 01:00:00 UTC 2026
Running Log Rotation...
Compressed files: 2
Deleted files: 0
Running Backup...
Backup created successfully!
Archive Name: backup-2026-06-07.tar.gz
Archive Size: 4.0K
Maintenance Completed: Sat Jun 07 01:00:03 UTC 2026
====================================
```

## Cron Entry

Run maintenance script daily at 1:00 AM:

```cron
0 1 * * * /home/ubuntu/day19-scripting/task4/maintenance.sh
```

---

# What I Learned

### 1. File Automation Using Shell Scripts

Learned how to automate log rotation and server backups using Bash scripting.

### 2. Scheduling Jobs with Cron

Learned cron syntax and how to schedule recurring jobs at specific times.

### 3. System Maintenance Automation

Learned how to combine multiple scripts into a single maintenance workflow and store logs for monitoring and troubleshooting.

---

# Conclusion

This project demonstrated practical Linux administration tasks including log management, backup automation, cron scheduling, and maintenance scripting. These skills are commonly used by DevOps Engineers, System Administrators, and Site Reliability Engineers to automate routine server operations.

```
```
