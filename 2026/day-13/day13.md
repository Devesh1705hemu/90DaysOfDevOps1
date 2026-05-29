🎯 Objective

# Learn Linux Logical Volume Management (LVM) to create, manage, mount, and extend storage volumes dynamically.

📋 Task 1: Check Current Storage
Commands Used
lsblk
pvs
vgs
lvs
df -h
Command Uses
Command	Purpose
lsblk =	Lists all available block devices, partitions, and mount points.
pvs =	Displays information about Physical Volumes (PV).
vgs =	Displays information about Volume Groups (VG).
lvs =	Displays information about Logical Volumes (LV).
df -h	 = Shows mounted filesystems and available disk space in human-readable format.


Outcome

Verified the current disk layout, mounted filesystems, and existing LVM configuration.

# Task 2: Create a Physical Volume (PV)
Command Used
pvcreate /dev/sdb
pvs
Command Uses
Command	Purpose
pvcreate /dev/sdb	 = Initializes the disk as a Physical Volume for LVM.
pvs = 	Verifies that the Physical Volume was created successfully.

Outcome

Successfully created a Physical Volume on the selected disk.

# Task 3: Create a Volume Group (VG)
Command Used
vgcreate devops-vg /dev/sdb
vgs
Command Uses
Command	Purpose
vgcreate devops-vg /dev/sdb =	Creates a Volume Group named devops-vg.
vgs =	Verifies the Volume Group details.

Outcome

Created a Volume Group that will serve as a storage pool for Logical Volumes.

# Task 4: Create a Logical Volume (LV)
Command Used
lvcreate -L 500M -n app-data devops-vg
lvs
Command Uses
Command	Purpose
lvcreate -L 500M -n app-data devops-vg =	Creates a 500 MB Logical Volume named app-data.
lvs =	Displays information about the created Logical Volume.

Outcome

Successfully created a Logical Volume inside the Volume Group.

# Task 5: Format and Mount the Logical Volume
Commands Used
mkfs.ext4 /dev/devops-vg/app-data

mkdir -p /mnt/app-data

mount /dev/devops-vg/app-data /mnt/app-data

df -h /mnt/app-data
Command Uses
Command	Purpose
mkfs.ext4 /dev/devops-vg/app-data =	Creates an ext4 filesystem on the Logical Volume.
mkdir -p /mnt/app-data =	Creates a directory to be used as a mount point.
mount /dev/devops-vg/app-data /mnt/app-data	 = Mounts the Logical Volume to the specified directory.
df -h /mnt/app-data =	Verifies the mounted filesystem and available storage.

Outcome

Successfully formatted and mounted the Logical Volume for use.

# Task 6: Extend the Logical Volume
Commands Used
lvextend -L +200M /dev/devops-vg/app-data

resize2fs /dev/devops-vg/app-data

df -h /mnt/app-data
Command Uses
Command	Purpose
lvextend -L +200M /dev/devops-vg/app-data =	Increases the Logical Volume size by 200 MB.
resize2fs /dev/devops-vg/app-data =	Expands the ext4 filesystem to utilize the new space.
df -h /mnt/app-data =	Confirms the filesystem size increase.

Outcome

Successfully extended the Logical Volume and resized the filesystem without recreating it.

# LVM Architecture
Physical Disk
      ↓
Physical Volume (PV)
      ↓
Volume Group (VG)
      ↓
Logical Volume (LV)
      ↓
Filesystem (ext4)
      ↓
Mount Point
#  What I Learned
1. Physical Volumes (PV)

Physical Volumes are disks or partitions initialized for LVM management.

2. Volume Groups (VG)

Volume Groups combine one or more Physical Volumes into a single storage pool.

3. Logical Volumes (LV)

Logical Volumes are flexible storage units that can be resized dynamically without repartitioning disks.

💡 Key Takeaways
Learned how to manage storage using Linux LVM.
Created Physical Volumes, Volume Groups, and Logical Volumes.
Formatted and mounted a Logical Volume.
Extended a Logical Volume without affecting existing data.
Understood the flexibility and scalability offered by LVM.
