# Process checks(commands)

1. Check running processes

use :  Shows all running processes in the system

command : ps aux | head

output 


2. Monitor live processes

use: Displays real time CPU, memory, and process activity.

command  :    top

output 

3. Find process by name

use:  Finds process ID of a specific running process.

command : pgrep sshd(process name)

output

 # Service Checks
1. Check SSH service status

Use: Checks whether a service is active or failed.

command: systemctl status ssh

output :

2. List running services


Use: Displays all currently running system services.


Command : systemctl list-units --type=service --state=running

Output :


3. View SSH logs


Use: Shows logs related to a specific service.


Command : journalctl -u ssh --no-pager | tail -n 5


Output: 

4. View recent system logs


Use: Displays the latest system log entries.


Command : tail -n 50 /var/log/syslog

Output: 


#  Service Inspection

Inspected Service: SSH


Purpose =
SSH allows secure remote login and server access.

Commands Used

Command	Use : 

systemctl status ssh	Checks SSH service status

journalctl -u ssh	Shows SSH related logs

pgrep sshd	Verifies SSH process is running

Observations: 

SSH service was running

SSH process existed

Logs showed successful login activity


# Mini Troubleshooting Steps
Step	Command	Use :

1	systemctl status ssh	=  Check service condition

2	sudo systemctl restart ssh = 	Restart SSH service

3	`journalctl -u ssh --no-pager = 	tail`

4	pgrep sshd	 = Verify SSH process

5	ssh user@localhost	 = Test SSH connection
