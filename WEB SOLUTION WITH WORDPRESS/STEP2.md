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
1.
````
lsblk
````
2.
````
sudo gdisk /dev/xvdf
