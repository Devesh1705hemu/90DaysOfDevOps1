****** Core components of Linux ****************
 
 # Linux Kernal
 The kernel is the core part of the Linux operating system. It acts as a bridge between hardware and software. It manages system resources and controls communication between hardware and applications.There are different types of kernels, but Linux uses a Monolithic Kernel.
 # User Spacce
 User space is the area where user applications and programs run. It is separate from the kernel space for security and stability.
Programs in user space cannot directly access hardware. They request services from the kernel through system calls.
# Init / systemd
Init is the first process started by the Linux kernel during booting. Its Process ID is PID 1. It initializes the system and starts background services.
Modern Linux distributions mainly use systemd instead of traditional init systems.



# Process States

A process is a program that is currently running in Linux.
A process changes its state while working.
# Running
The process is actively using the CPU and executing instructions.
# Ready
The process is ready to run but waiting for CPU time.
# Sleeping (Waiting)
The process is waiting for some event like user input, file reading, or network response.
# Stopped
The process is paused or stopped temporarily.
# Zombie
The process has finished execution but still has an entry in the process table because the parent process has not removed it yet.
# Dead (Terminated)
The process is completely finished and removed from memory.

# Process Management
Linux manages processes by:
Giving each process a unique PID (Process ID)
Allocating CPU and memory
Scheduling process execution
Stopping or ending processes when needed
Useful commands:
ps        # show running processes
top       # live process monitoring
kill PID  # stop a process

# systemd 
systemd is the modern system and service manager in Linux. It is the first process started after the kernel boots.
What systemd Does:
Starts system services during boot
Manages background services (daemons)
Restarts failed services automatically
Handles logging and system startup
Improves boot speed using parallel startup
Why It Matters:
Faster and more organized boot process
Better control over services
Automatic service recovery
Easy service management using systemctl.
systemd is important because it keeps the Linux system running smoothly and manages all essential services efficiently.

# Architecture of Linux
A = Application
S = Shell
K = kernel 

# Linux Commands for daily uses 
pwd      # show current directory
ls       # list files and folders
cd       # change directory
mkdir    # create new folder
touch    # create empty file
vim      # open and edit files
cat      # display file content
head     # show first lines of a file
tail     # show last lines of a file
echo     # print text on terminal
man      # show command manual/help

# Today task 
Create a folder.
cd into that folder
write into that folder
show the file content
use vim to edit file
then save the file
show file content again






