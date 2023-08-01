# SSH into the database server to install mysql database.
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
Create a passpord for the database.
Answer y to all questions.
````
sudo mysql -u root -p
````
Configure DB to work with WordPress
````
CREATE DATABASE wordpress;
  show database;
CREATE USER `wordpress`@`%' IDENTIFIED WITH mysql_native_password BY 'wordpress';
GRANT ALL ON *.* TO 'wordpress'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit
````
To check if the host has been created run:
````
select user, host from mysql.user
exit
````
Note: % means the user can be connected from anywhere.
localhost means this machine only.

# SETTING THE BIND ADDRESS.
````
sudo vi /etc/my.cnf
````


