# Linux Commands CheatSheat
_____________________________________
# Process Management Commands
Viewing Processes
ps                  # Show current processes
ps aux              # Show all running processes
top                 # Live process monitoring
htop                # Interactive process viewer
pidof process_name  # Find process ID

Killing Processes
kill PID            # Stop process
kill -9 PID         # Force kill process
pkill process_name  # Kill process by name
xkill               # Kill GUI application

# Background & Foreground Process Management
jobs                # Show background jobs
bg                  # Run stopped job in background
fg                  # Bring job to foreground
nohup command &     # Run process after logout

# Process Priority Management
nice -n 10 command  # Start process with priority
renice 5 PID        # Change process priority

# System Performance Monitoring
free -h             # Check memory usage
uptime              # Show uptime and load
vmstat              # Virtual memory statistics

# Service & Daemon Management
systemctl status service   # Check service status
systemctl start service    # Start service
systemctl stop service     # Stop service
systemctl restart service  # Restart service
systemctl enable service   # Enable service at boot

_______________________________________________________________________

# File System Commands
_____________________________________
# File & Directory Navigation
pwd                 # Show current directory
ls                  # List files and folders
ls -l               # Detailed file list
cd directory_name   # Change directory

# File Creation & Editing
touch file.txt      # Create empty file
vim file.txt        # Edit file
nano file.txt       # Open file in nano editor

# File Operations
cp file1 file2      # Copy file
mv file1 file2      # Move/Rename file
rm file.txt         # Delete file
rm -r folder        # Delete folder recursively

# File Viewing
cat file.txt        # Show file content
head file.txt       # First 10 lines
tail file.txt       # Last 10 lines
less file.txt       # View file page by page

# File Permissions
chmod 755 file      # Change permissions
chown user file     # Change file owner

# Disk Usage
df -h               # Disk space usage
du -sh folder       # Folder size

# File Searching
find / -name file   # Search file
grep "text" file    # Search text in file
 ________________________________________________________________________-
 # Networking Troubleshooting Commands
 ________________________________________________
 # Network Information
ip a                # Show IP address
hostname            # Show system hostname
ifconfig            # Network interface details

# Connectivity Testing
ping google.com     # Test internet connectivity
traceroute google.com # Show network path
mtr google.com      # Network diagnostics

# DNS Troubleshooting
nslookup google.com # DNS lookup
dig google.com      # Detailed DNS info

# Port & Connection Checking
netstat -tulnp      # Show open ports
ss -tulnp           # Socket statistics
lsof -i :80         # Check process using port

# Download & Request Testing
curl google.com     # Send HTTP request
wget url            # Download file

# Service Troubleshooting
systemctl status NetworkManager  # Check network service
restart networking   # Restart network service
________________________________________________________________________________________________________________
# Essential Networking Troubleshooting Commands 

ping google.com         # Check connectivity
ip addr                 # Show IP addresses
ss -tulnp               # Show open ports and services
dig google.com          # DNS lookup
curl http://site.com    # Test HTTP response
traceroute google.com   # Show network path
netstat -tulnp          # Display listening ports
nc -zv host port        # Test port connectivity
tcpdump -i eth0         # Capture network packets
ip route                # Show routing table
___________________________________________________________________




# Daily Useful DevOps Commands By chatgpt
__________________________________________
# File System Commands
pwd                     # Show current directory
ls -la                  # List all files with details
cd directory            # Change directory
mkdir folder            # Create directory
rm -rf folder           # Remove directory/files
cp file1 file2          # Copy files
mv file1 file2          # Move/Rename files
find / -name file       # Search files
grep "text" file        # Search text in file
chmod 755 file          # Change permissions
chown user:user file    # Change ownership
df -h                   # Disk usage
du -sh folder           # Folder size
tail -f logfile         # Monitor logs live

# Process Management Commands
ps aux                  # Show running processes
top                     # Live process monitoring
htop                    # Interactive process viewer
kill PID                # Stop process
pkill process           # Kill process by name
systemctl status nginx  # Check service status
systemctl restart nginx # Restart service
journalctl -u nginx     # View service logs

# Networking Commands
ping google.com         # Check connectivity
ip addr                 # Show IP address
ss -tulnp               # Show open ports
netstat -tulnp          # Display network connections
dig google.com          # DNS lookup
curl http://site.com    # Test HTTP response
traceroute google.com   # Trace network path
nc -zv host port        # Check port connectivity
tcpdump -i eth0         # Capture packets
ip route                # Show routing table

# User Management Commands
whoami                  # Current user
id                      # User and group IDs
useradd username        # Create user
passwd username         # Set password
usermod -aG group user  # Add user to group
sudo command            # Run as root

# Package Management Commands
apt update              # Update package list
apt install nginx       # Install package
apt remove nginx        # Remove package
yum install nginx       # Install package in RHEL/CentOS

# Archive & Compression Commands
tar -cvf file.tar dir   # Create tar archive
tar -xvf file.tar       # Extract tar archive
zip -r file.zip dir     # Create zip file
unzip file.zip          # Extract zip file

# DevOps & Monitoring Commands
docker ps               # Running containers
docker logs container   # Container logs
docker exec -it cont bash # Access container
kubectl get pods        # List Kubernetes pods
kubectl logs pod        # Pod logs
free -h                 # Memory usage
uptime                  # System uptime
vmstat                  # System performance stats
