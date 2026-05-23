# Linux File System Hierarchy Notes

---

## `/` Root Directory

### What it contains

The root directory is the starting point of the Linux file system.
All files and directories exist under this directory.

### Command

```bash id="ddr5uk"
ls -l /
```

### Example Files/Folders Seen

```bash id="szl43v"
home
etc
var
```

### I would use this when...

I want to navigate the complete Linux system structure.

---

## `/home`

### What it contains

This directory stores personal files and folders of normal users.
Each user gets a separate home directory.

### Command

```bash id="nbyqxr"
ls -l /home
```

### Example Files/Folders Seen

```bash id="48wtwy"
devesh
ubuntu
```

### I would use this when...

I need to access user projects, downloads, and personal files.

---

## `/root`

### What it contains

This is the home directory of the root user (administrator).
It contains root user's personal and configuration files.

### Command

```bash id="n8kgtr"
sudo ls -l /root
```

### Example Files/Folders Seen

```bash id="h5q0ma"
.bashrc
.cache
```

### I would use this when...

I need administrator-level access and server management tasks.

---

## `/etc`

### What it contains

This directory stores system configuration files.
Linux services and applications keep their settings here.

### Command

```bash id="zzxjdf"
ls -l /etc
```

### Example Files/Folders Seen

```bash id="vzfq5v"
hostname
ssh
passwd
```

### I would use this when...

I need to configure services, networking, or system settings.

---

## `/var/log`

### What it contains

This directory stores system and application log files.
Logs help in troubleshooting and monitoring servers.

### Command

```bash id="6h0mpq"
ls -l /var/log
```

### Example Files/Folders Seen

```bash id="w3jl2u"
syslog
auth.log
```

### I would use this when...

I need to investigate errors or monitor application activity.

---

## `/tmp`

### What it contains

This directory stores temporary files created by applications and users.
Files may be deleted automatically after reboot.

### Command

```bash id="f6m2nq"
ls -l /tmp
```

### Example Files/Folders Seen

```bash id="9v6m4r"
systemd-private
tmpfile
```

### I would use this when...

I need temporary storage during testing or script execution.

---

## `/bin`

### What it contains

This directory contains essential Linux command binaries.
Basic commands required for system operation are stored here.

### Command

```bash id="4w7dzc"
ls -l /bin
```

### Example Files/Folders Seen

```bash id="u8y0mr"
ls
cp
mv
```

### I would use this when...

I need to execute important Linux commands for daily operations.

---

## `/usr/bin`

### What it contains

This directory stores user-level application binaries and installed software commands.

### Command

```bash id="3fh6qa"
ls -l /usr/bin
```

### Example Files/Folders Seen

```bash id="9m4dqy"
python3
git
nano
```

### I would use this when...

I need to run installed software and development tools.

---

## `/opt`

### What it contains

This directory is used for optional or third-party software installations.

### Command

```bash id="mg6z8f"
ls -l /opt
```

### Example Files/Folders Seen

```bash id="2sjm0d"
google
containerd
```

### I would use this when...

I install and manage external applications or enterprise software.



# Scenario-Based Linux Troubleshooting Practice

---

# Scenario 1: Service Not Starting

## Problem

A web application service called `myapp` failed to start after a server reboot.

---

## Step 1

```bash id="pzj1r6"
systemctl status myapp
```

### Why

Checks whether the service is running, stopped, or failed.

---

## Step 2

```bash id="t5k3qa"
journalctl -u myapp -n 50
```

### Why

Displays the latest 50 log lines related to the service to identify errors.

---

## Step 3

```bash id="7o8mrx"
systemctl is-enabled myapp
```

### Why

Checks whether the service is configured to start automatically after reboot.

---

## Step 4

```bash id="ux6k1m"
systemctl list-units --type=service
```

### Why

Lists all available services to verify whether `myapp` exists.

---

## Step 5

```bash id="w4y2zn"
sudo systemctl restart myapp
```

### Why

Attempts to restart the service after checking logs and status.

---

## Step 6

```bash id="6e1vko"
sudo journalctl -xe
```

### Why

Shows detailed system error logs for deeper troubleshooting.

---

# What I Learned

Always start by checking service status, then inspect logs, verify boot configuration, and finally attempt recovery actions like restart.

---

# Scenario 2: High CPU Usage

## Problem

The application server is slow and may have high CPU usage.

---

## Step 1

```bash id="v7q5ls"
top
```

### Why

Shows live CPU and memory usage of running processes.

### Note

Press `q` to quit.

---

## Step 2

```bash id="x8p2jw"
ps aux --sort=-%cpu | head -10
```

### Why

Displays the top 10 processes consuming the highest CPU.

---

## Step 3

```bash id="h2w9dn"
htop
```

### Why

Provides an interactive and easier-to-read process monitoring interface.

### Note

Press `q` to quit.

---

## Step 4

```bash id="g4m7xy"
ps -p PID -o %cpu,%mem,cmd
```

### Why

Checks detailed CPU, memory, and command information for a specific process.

### Example

```bash id="9z4bke"
ps -p 1234 -o %cpu,%mem,cmd
```

---

## Step 5

```bash id="v1k6rs"
uptime
```

### Why

Shows system load average to understand overall server load.

---

## Step 6

```bash id="c8q3lf"
free -h
```

### Why

Checks memory usage because high memory usage can also slow the server.

---

# What I Learned

When troubleshooting performance issues, first identify high CPU-consuming processes, inspect their PID, check system load, and verify whether memory usage is also affecting performance.


# Scenario 3: Finding Service Logs

## Problem

A developer asks: "Where are the logs for the `docker` service?"

The service is managed by `systemd`.

---

## Step 1

```bash id="7m2qkp"
systemctl status docker
```

### Why

Checks whether the Docker service is running, failed, or stopped and shows recent log entries.

---

## Step 2

```bash id="x5v8ld"
journalctl -u docker -n 50
```

### Why

Displays the last 50 log lines of the Docker service for troubleshooting.

---

## Step 3

```bash id="4k9wzt"
journalctl -u docker -f
```

### Why

Follows Docker logs in real-time and helps monitor live service activity.

### Note

Press `Ctrl + C` to stop following logs.

---

## Step 4

```bash id="q3d6yn"
journalctl -u docker --since "1 hour ago"
```

### Why

Shows Docker logs generated within the last one hour.

---

## Step 5

```bash id="n8p4vs"
journalctl -u docker --since today
```

### Why

Displays all Docker service logs generated today.

---

## Step 6

```bash id="b1x7rm"
sudo journalctl -xe
```

### Why

Checks detailed system-wide error logs related to services and failures.

---

# What I Learned

For `systemd` services, logs are mainly stored in `journald`.
Start by checking service status, then use `journalctl` to inspect recent logs, monitor live activity, and investigate errors based on time.



# Scenario 4: File Permissions Issue

## Problem

A script located at `/home/user/backup.sh` is not executing.

Error received:

```bash id="t5v9pk"
Permission denied
```

---

## Step 1: Check Current Permissions

```bash id="d3m7qx"
ls -l /home/user/backup.sh
```

### Why

Checks the current permissions of the script file.

### Look For

```bash id="r8k2zn"
-rw-r--r--
```

Notice there is no `x` permission, meaning the file is not executable.

---

## Step 2: Add Execute Permission

```bash id="v1x6cf"
chmod +x /home/user/backup.sh
```

### Why

Adds execute permission to the script so it can run as a program.

---

## Step 3: Verify Permissions Again

```bash id="m4q8la"
ls -l /home/user/backup.sh
```

### Why

Confirms that execute permission was successfully added.

### Look For

```bash id="k7n2wd"
-rwxr-xr-x
```

Notice the `x` permission is now present.

---

## Step 4: Run the Script

```bash id="p9z5ut"
./backup.sh
```

### Why

Executes the script after fixing permissions.

---

## Step 5: Check File Owner (Optional Troubleshooting)

```bash id="x2f6mr"
ls -l /home/user/
```

### Why

Verifies file ownership and permissions inside the directory.

---

## Step 6: Change Ownership if Needed

```bash id="g5v3nc"
sudo chown user:user /home/user/backup.sh
```

### Why

Changes the file owner if permission issues are caused by incorrect ownership.

---

# What I Learned

Linux files need execute (`x`) permission to run as scripts or programs.
Always check permissions first using `ls -l`, then fix them using `chmod +x` before troubleshooting further.

