# INSTALLING SQL #
This satge we have installed our Apache webserver and we have it running, This process will detail the installation of our Database Management System (DBMS), which will enable us store and manage data for the website in a relational database. My SQL is a very popular relational datbase used within PHP environments.

* Run the following command with the Ubuntu package manager 'apt' 
````
$ sudo apt install mysql-server
````
When prompted, type Yes to confirm installation.

Once the installation is complete, enter the following command to access the MySQL console:

````
$ sudo mysql
````

This connects to the MySQL server as the administrative database user root, which is implied by the fact that this command is executed with sudo. 
The following output should show;

````
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.22-0ubuntu0.20.04.3 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
````
Running the security script that comes pre-installed with MySQL is advised. This script will lock down access to your database system and remove several unsafe default settings. You must create a password for the root user before executing the script, with mysql_native_password serving as the default authentication mechanism. The password for this user is defined as PassWord.1.

````
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
````
* Run this commnd to exit the MySql shell; 
````
mysql> exit
````
* Run this script to start the security installation script; 
````
$ sudo mysql_secure_installation
````
You will be prompted to configure the VALIDATE PASSWORD PLUGIN.

The decision to enable this feature is quite subjective. If enabled, MySQL will reject passwords with an error if they don't meet the specified criteria. Validation can be stopped without risk, but you should always use secure, one-of-a-kind passwords for database logins. The validation process can be quite tedious, so it is subjective to each person andhe hevel of secruity protocol you would like to create for granting access to your database.

To continue without enabling, respond with Y for yes or with anything else.
````
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:
````
You will be prompted to choose a level of password validation if you respond "yes." Remember that if you choose the strongest level of 2 and try to make a password that doesn't include numbers, upper and lowercase letters, special characters, or is based on a common dictionary word, like PassWord.1, you will get errors.
````
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
````
Your server will then request that you choose and confirm a password for the MySQL root user, regardless of whether you decided to configure the VALIDATE PASSWORD PLUGIN. Contrast this with the system root to avoid confusion. The database root user has complete control over the database system and is an administrator user. Even though the MySQL root user's default authentication method disallows the use of passwords even when they are set, you should define a strong password here as an extra layer of security. In a bit, we'll talk about this.


If you enabled password validation, your server will ask you if you still want to use the root password after displaying the root password's password strength. If the screen asks if you're satisfied with your password, type Y for "yes" to respond:

````
Estimated strength of the password: 100 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
````
For the rest of the questions, press Y and hit the ENTER key at each prompt. This will prompt you to change the root password, remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes you have made.

* Run this command to test if you can log into the MYSQl console;
````
$ sudo mysql -p
````
Notice the -p flag in this command, which will prompt you for the password used after changing the root user password.

To exit the MySQL console, type:
````
mysql> exit
````
Notice that you need to provide a password to connect as the root user.

For increased security, it’s best to have dedicated user accounts with less expansive privileges set up for every database, especially if you plan on having multiple databases hosted on your server.

Note: At the time of this writing, the native MySQL PHP library mysqlnd doesn’t support caching_sha2_authentication, the default authentication method for MySQL 8. For that reason, when creating database users for PHP applications on MySQL 8, you’ll need to make sure they’re configured to use mysql_native_password instead.

Your MySQL server is now installed and secured. Next, we will install PHP, the final component in the LAMP stack.
