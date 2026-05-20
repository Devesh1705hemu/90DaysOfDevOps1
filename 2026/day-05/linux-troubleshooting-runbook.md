# Target Service / Process

Service chosen: OpenSSH (sshd)

Purpose: Verify service health, system resources, network state, and logs during troubleshooting.

# Snapshot: Environment Basics

1. System Information

Command    = uname -a


Use:
Shows kernel version, OS architecture, and system details.


2. OS Release Details

Command =    cat /etc/os-release

Use:    Displays Linux distribution and version information.


# Filesystem Sanity Check
1. Create Temporary Directory
   
Command =mkdir /tmp/runbook-demo

Use:   Creates a temporary folder for testing filesystem operations.


2. Copy File and Verify

Command = cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo


Use:    Copies a file and verifies file permissions and storage access.


# Snapshot: CPU & Memory
1. Check Memory Usage

Command =   free -h

Use:  Displays RAM and swap memory usage in human-readable format.



2. Inspect SSH Process Usage

Command = ps -o pid,pcpu,pmem,comm -C sshd

Use:   Shows CPU and memory consumption of the SSH service.


 # Snapshot: Disk & IO
1. Disk Space Check

   
Command  = df -h

Use:  Checks available and used disk space on mounted filesystems.



2. Check Log Directory Size

   
Command =   du -sh /var/log

Use:   Calculates total disk usage of log files.



# Snapshot: Network
1. Verify Listening Ports

Command = ss -tulpn | grep ssh

Use:   Checks whether SSH service is listening on network ports.

2. Test Local Connectivity

Command =  curl -I http://localhost

Use:  Sends an HTTP request to verify local server/network response.

# Logs Reviewed
1. Review SSH Logs

Command =  journalctl -u ssh -n 20

Use:   Displays the latest logs from the SSH service.


2. Check System Logs

Command = tail -n 20 /var/log/syslog

Use:  Shows the most recent system log entries.



 # If This Worsens 
 
1. Restart Service

Command =   sudo systemctl restart ssh

            sudo systemctl status ssh

Use:   Restarts SSH service and verifies current status.

2. Monitor Live Logs

Command = sudo journalctl -u ssh -f

Use:   Tracks SSH logs in real time for failures or crashes.

3. Trace Service Activity

Command = sudo strace -p <PID>

Use:   Monitors system calls to diagnose hangs or blocked operations.
