1. # LAUNCH TWO EC2 INSTANCES.
Server A - WEBSERVER (WORDPRESS)
Server B - DATABASE SERVER (MYSQL)

* Launch those instances using the redhat distribution for the operating system.
* Confirm the availability zones for both instance on the management console.
2. Navigate to the Elastic Block Store, then Volumes.
* Create three EBS volumes for the both instance created, sizes 10gb each , set availability zone to the same one the instance is running on .
* Click on Create Volume.
* Name the three instance for the webserver web1, web2, web3.
* Name the three instance for the database server datab1, datab2,datab3.
  
* # Attach the volumes to their instances.
* Click on the volume, ``ACTIONS``, ``ATTACH VOLUMES``, SEARCH FOR THE INSTANCE EG ``WEBSERVER OR DATABASES``.
* cLICK ON IT AND ``ATTACH``.
* Repeat the process for all 6 EBS volumes.
  
![Screenshot 2023-07-31 at 20 16 22](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/0e4f5cdc-58eb-43f2-b017-b77e5cb4246a)

3. # SSH INTO THE WEBSERVER TERMINAL.
Note: Don't forget to use ec2-user@<public-ip> for redhat OS.
Update the server:
````
sudo yum -y update
````
Run this command:
````
lsblk
````
![Screenshot 2023-07-31 at 22 46 18](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/cf0d5388-5c34-4c3d-80fb-34b49db41360)


4. This function is used to view and confirm the three EBS volumes that were previously created.
USE:
````
df-h
````
* This is used to view the mount point available.

Note: We are creating a partition on the three physical disks using gdisk, then switch into logical volume management(LVM). In order to create the LVM, we need to firts create the physical disk, then concatenante into the volume group then makes the logical volume.
START BY CREATING THE PARTTION ON EACH DISK .
5.USE:
````
gdisk
````
6. This is the used to create partition on the three disks.
USE:
````
sudo gdisk /dev/xvdf
````
Next, you will see a prompt :
````
Command (? for help): n
````
Note: n means new partition.
````
Partition number (1-128, default.1): 1
First Sector (34- 20971486, default = 2048) or {+-} size {KMGTP} : <Click enter>
Note: This means the size at which you want the disk to be used for to which if indicated :4 means 4gb but was left blank inorder to use total size.
Last Sector (2048-209714861----) <also click enter>
Current type is 'Linux Filesystem'
Note: We want to change this to LVM and we do that by:
Hex Code or GUID : 8e00
This changes the partition type to 'Linux LVM'
 GPT fdisk (gdisk) version 1.0.3

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries.

Command (? for help branch gloryE-edits: p
Not: Use p tp verify all we just did.
Disk /dev/xvdf: 20971520 sectors, 10.0 GiB
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): D936A35E-CE80-41A1-B87E-54D2044D160B
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 20971486
Partitions will be aligned on 2048-sector boundaries
Total free space is 2014 sectors (1007.0 KiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048        20971486   10.0 GiB    8E00  Linux LVM

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): yes
OK; writing new GUID partition table (GPT) to /dev/xvdf.
The operation has completed successfully.
Now,  your changes has been configured succesfuly, exit out of the gdisk console and do the same for the remaining disks.
````
7. Use lsblk utility to view the newly configured partition on each of the 3 disks.
````
lsblk
````
![Screenshot 2023-07-31 at 23 02 23](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/dae02091-a46f-4fed-ad6c-5ba3812e4484)

8. Install lvm2 package using:
````
sudo yum install lvm2 -y
````
9. Verify it has been insatlled by running
````
which lvm
````
Note: In Ubuntu we used apt command to install packages, in RedHat/CentOS a different package manager is used, so we shall use yum command instead.
10. # CREATE A PHYSICAL VOLUME ON 3 DISKS.
You can only create physical volumes in partitions.
````
sudo pvcreate /dev/xvdf1 /dev/xvdg1 /dev/xvdh1
````
11. Verify that your Physical volume has been created successfully by running 
````
sudo pvs
````
![Screenshot 2023-07-31 at 23 08 52](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/80a5e749-400b-466e-a168-067f53a43017)

* # NEXT WE WANT TO ADD VOLUME GROUPS.
Volume groups means combining disks together as one. (combination of the three ebs disks) because LVM can only reside in a volume group.

12. Use vgcreate utility to add all 3 PVs to a volume group (VG). Name the VG vg-webdata
````
sudo vgcreate vg-webdata /dev/xvdf1 /dev/xvdg1 /dev/xvdh1
````
13. Verify that your VG has been created successfully by running
````
sudo vgs
````

![Screenshot 2023-07-31 at 23 17 01](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/6ae256ac-f192-41e9-9b60-ac93da8fb6d4)

* # CREATE THE LOGICAL VOLUME.
This is the volume given to ther servers. In this project, i will be creating two logical volumes called apps-lv and logs-lv.
Note: apps-lv would be used to store data from the website, while logs-lv will be used to store data for logs.
14. Use lvcreate utility to create 2 logical volumes. apps-lv (Use half of the PV size), and logs-lv Use the remaining space of the PV size.
````
sudo lvcreate -n apps-lv -L 14G vg-webdata
sudo lvcreate -n logs-lv -L 14G vg-webdata
````
15. Verify that your Logical Volume has been created successfully by running:
````
sudo lvs
````
![Screenshot 2023-07-31 at 23 25 47](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/b9a08dad-076a-4886-982e-5735110d4c8b)

16.Verify the entire setup
````
sudo vgdisplay -v #view complete setup - VG, PV, and LV
sudo lsblk
````
With LVM we just created a device, Now we need to add a filesystem to it.

17. Use mkfs.ext4 to format the logical volumes with ext4 filesystem
````
sudo mkfs.ext4 /dev/vg-webdata/apps-lv
sudo mkfs.ext4 /dev/vg-webdata-vg/logs-lv
````
18. CREATE MOUNT POINTS FOR THE DEVICES.
Firstly, check if /var/www exists by running:
````
sudo ls -l
````
19. Create /var/www/html directory to store website files:
````
sudo mkdir -p /var/www/html
````
20.Create /home/recovery/logs to store backup of log data:
````
sudo mkdir -p /home/recovery/logs
````
21.Before mounting a directory it is safe pratcse to always check if there are files on it, if not during mounting all the files will be deleted. In order to do that run:
````
ls -l /var/wwww/html
````
Note: if its total 0
Mount /var/www/html on apps-lv logical volume:
Note: This means that whatever is stored in the /var/www/html will also be stored in the apps-lv.
22. Mount the file by running :
````
sudo mount /dev/vg-webdata/apps-lv /var/www/html/
````
23. Verify that it has been mounted by running :
````
df-h
````
24. Again, for safe prtaicse check the file before mounting the log file:
````
sudo ls-l /var/logs 
````
* You will see some contents that are very important.
25. Before mounting on /var/logs copy the docs to /home/recovery/logs using:
````
sudo rsync -av /var/log/. /home/recovery/logs/
````
26. To verify that it was copied or backed up RUN:
 ````
 sudo ls -l /home/recovery/logs/
 sudo ls -l /home/recovery/logs/log
 ````
27. Mount /var/log on logs-lv logical volume.
````
sudo mount /dev/vg-webdata/logs-lv /var/log
````
28.Restore copied log files back to /var/log.
````
sudo rsync -av /home/recovery/logs/log/ /var/log
````
29. Verify that it has been backed up:
````
sudo ls -l /var/log
````
30.Verify the mounts.
````
df-h
````
Note: Although it has been mounted, it is a temporary mout if the server is restarted it will be deleted in other to make it persistent.



