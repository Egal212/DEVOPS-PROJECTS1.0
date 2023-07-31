Note: Although it has been mounted, it is a temporary mout if the server is restarted it will be deleted in other to make it persistent.
Update /etc/fstab file so that the mount configuration will persist after restart of the server. Click on the next Step To update the /etc/fstab file
# UPDATE THE /ETC/FSTAB FILE
1. Check the block ID:
````
sudo blkid
````
![Screenshot 2023-08-01 at 00 00 00](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/ca4fb099-3288-42a0-aade-cc38a56c23d1)
Note: The UUID on the apps-lv is equivalent to the LV SO cope and save on a notepad.
2. VI into the file
````
sudo vi /etc/fstab
````
Update /etc/fstab in this format using your own UUID and rememeber to comment #mount for wordpress webserver
and remove the leading and ending quotes.

![Screenshot 2023-08-01 at 00 02 12](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/6aa32d12-8335-4c9e-a3f9-b78d8c3d88b9)

3. Test the configuration and reload the daemon
````
sudo mount -a
sudo systemctl daemon-reload
````
4. Verify your setup by running df -h, output must look like this:
 ````
   df-h!
````

![Screenshot 2023-08-01 at 00 10 23](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/71cf756d-9ec3-4fc0-87fc-b88b0f51bb0c)


NOW FOR THE DATABASE SERVER.

Prepare the Database Server Launch a second RedHat EC2 instance that will have a role – ‘DB Server’ Repeat the same steps as for the Web Server, but instead of apps-lv create db-lv and mount it to /db directory instead of /var/www/html/.

* Create the EBS Volume  and attach if you havent previusly done it.

* SSH INTO THE DATABASE SERVER.
Run the following commands:
````
lsblk
````
This function is used to view and confirm the three EBS volumes that were previously created. USE:
````
df-h
````
This is used to view the mount point available.
Note: We are creating a partition on the three physical disks using gdisk, then switch into logical volume management(LVM). In order to create the LVM, we need to firts create the physical disk, then concatenante into the volume group then makes the logical volume. START BY CREATING THE PARTTION ON EACH DISK . 5.USE:
````
gdisk
````
This is the used to create partition on the three disks. USE:
````
sudo gdisk /dev/xvdf
````
Next, you will see a prompt :
````
Command (? for help): n
Note: n means new partition.

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
Use lsblk utility to view the newly configured partition on each of the 3 disks.
````
lsblk
````
To install the lvm
````
sudo yum install lvm2 -y
````
CREATE THE PHYSICAL VOLUME
````
sudo pvcreate /dev/xvdf1 /dev/xdvfg1 /dev/xvdh1
````
CREATE THE VOLUME GROUP
````
sudo vgcreate vg-database /dev/xvdf1 /dev/xdvfg1 /dev/xvdh1
````
CREATE THE LOGICAL VOLUME
````
sudo vgs
sudo lvcreate -n db-lv -L 20G vg-database
sudo lvs
````
CREATE MOUNT POINTS
````
sudo mkdir /db
````
Before mounting make file systems
````
sudo mkfs.ext4 /dev/vg-database/db-lv
sudo ls -l /db
````
Mount using  this code:
````
sudo mount /dev/vg-database/db-lv /db
df -h
````
To make the mount persistent.
````
sudo blkid
````
Copy UUID
Update /etc/fstab
````
sudo vi /etc/fstab
````
#Comment mout for database
Paste the UUID remove the " " /db ext4 defaults 0 0
EXIT FROM VI USING :wqa!

Mount, restart the daemon and update the OS using:
````
sudo mount -a
sudo systemctl daemon -reload
df-h
sudo yum -y update
````



