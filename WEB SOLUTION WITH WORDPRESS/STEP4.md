#1. SSH into the database server to install mysql database.
At this point we are trying to connect the webserver mysql database to the mysqldatabase server.
````
sudo yum update
sudo yum install mysql-server
sudo systemctl restart mysqld
sudo systemctl enable mysqld
sudo systemctl status mysqld
sudo mysql_secure_installation
````
SAY NO: but if working for a real project set up password policies.
Create a password for the database.
2. Answer y to all questions.
````
sudo mysql -u root -p
````
3. Configure DB to work with WordPress
````
CREATE DATABASE wordpress;
  show database;
CREATE USER `wordpress`@`%' IDENTIFIED WITH mysql_native_password BY 'wordpress';
GRANT ALL ON *.* TO 'wordpress'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit
````
4. To check if the host has been created run:
````
select user, host from mysql.user
exit
````
Note: '%' means the user can be connected from anywhere.
localhost means this machine only.

5. # UPDATING THE BIND ADDRESS.
````
sudo vi /etc/my.cnf
````
Comment [mysqld]
bind address = 0.0.0.0
Note: if you indicate a particular ip address when creating the host indicate it here.
````
sudo systemctl restart mysqld
````

6. # NAVIGATE TO THE WEBSERVER TERMINAL.
Open the wp-config.php file
````
sudo vi wp-config.php
````
7. Navigate to //** Mysql settings: You will see this output:
````
/** The name of the database for wordpress define ('DB-NAME',"<replace this word with the name you want to name ur database eg. wordpress>'"):

Change the name of the username to the username of choice eg wordpress
define ('DB-USER', 'SET USERNAME HERE')

Change the name of the PASSWORD to the PASSWORD of choice eg password
define ('DB-PASSWORD', 'SET PASSWORD HERE')

Copy the private ip-address of database and change the hostname.
define ('DB-HOST', 'PLACE PRIVATE IP ADDRESS HERE')
````
8. # RESTART THE HTTPD.
````
sudo systemctl restart httpd
````
9. Dispable apache welcome page by Renaming the apache document from welcome.conf to welcome.conf.backup.
This enables the apache welcome page by renaming it.
````
sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf_backup
````
10. Confirm that you can connect from your Web Server to your DB server by using mysql-client
````
sudo mysql -h <DB-Server-Private-IP-address> -u wordpress -p
````
Input password
mysql> show databases;
````
sudo chown -R apache:apache /var/www/html/
ls -l
sudo chcon -t httpd_sys_rw_content_t /var/www/html/ -R
sudo setsebool -P httpd_can_network_connect=1
sudo setsebool -P httpd-can_network_connect_db 1
````
RELOAD THE APACHE WEBPAGE ; YOU WILL SEE THE WORDPRESS PAGE AND THIS OUTPUT.
SET YOUR USERNAME, PASSWORD AND EMAIL THEN INSTALL WORDPRESS AND LOGIN.
YOU CAN NOW BUILD YOUR DYNAMIC WEBSITE WITH WORDPRESS.

![Screenshot 2023-08-01 at 10 24 54](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/92a9f1a8-43ff-4d16-8fcf-36cc7505dca7)


![Screenshot 2023-08-01 at 10 25 40](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/48ca7f67-8709-4161-b8f9-677fa4cd6188)

NOW YOU HAVE A CONFIGURED WORDPRESS WEBSITE.


