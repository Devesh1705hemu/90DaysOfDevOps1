# ==============================
# Linux Command Cheat Sheet
# ==============================

# ------------------------------
# File System Commands
# ------------------------------

ls -la                 # List all files with details

cd directory           # Change directory

mkdir folder           # Create directory

touch file.txt         # Create empty file

rm -rf folder          # Remove files/folders

cp file1 file2         # Copy files

mv file1 file2         # Move/Rename files

find / -name file      # Search file 

grep "text" file       # Search text

chmod 755 file         # Change permissions

chown user:user file   # Change ownership

df -h                  # Disk usage

du -sh folder          # Folder size

tail -f logfile        # Live log monitoring

head file.txt          # Show first lines

cat file.txt           # Display file content


vim file.txt           # Open file in vim

nano file.txt          # Open file in nano

tar -czvf backup.tar.gz folder   # Compress folder

unzip file.zip         # Extract zip file

# ------------------------------
# Process Management Commands
# ------------------------------

ps aux                         # Show running processes

top                            # Live process monitoring

htop                           # Interactive process viewer

kill PID                       # Stop process

killall process_name           # Kill process by name

pkill process_name             # Kill process using pattern

jobs                           # Show background jobs

bg                             # Run job in background

fg                             # Bring job to foreground

nohup command &                # Run after logout

nice -n 10 command             # Start process with priority

renice 5 PID                   # Change process priority

free -h                        # Memory usage

uptime                         # System uptime

lsof -i                        # Open ports and connections

systemctl status nginx         # Check service status

systemctl restart nginx        # Restart service

journalctl -u nginx            # Service logs

# ------------------------------
# Networking Commands
# ------------------------------

ping google.com                # Check connectivity

ip addr                        # Show IP address

curl https://example.com       # Test HTTP response

dig google.com                 # DNS lookup

ss -tulnp                      # Show listening ports

netstat -tulnp                 # Active connections

traceroute google.com          # Trace network path

nslookup google.com            # Query DNS

wget URL                       # Download file

hostname -I                    # Show local IP


# ------------------------------
# Daily  Useful Commands
# ------------------------------

history                        # Show command history

clear                          # Clear terminal

whoami                         # Current user

uname -a                       # System information

date                           # Current date and time

env                            # Environment variables

echo "Hello"                   # Print output

man command                    # Open manual page


