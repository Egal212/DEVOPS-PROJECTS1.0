# INSTALLING LIPAPACHE2-MOD-PHP
Currently I have apache installed to serve my content and mysql installed to store and manage data.
Php is the resource that will help process code to display dynamic content to end user.
In addition to the php package, php-mysql had to be installed to communicate with mysql-based databases and 
libapache2-mod-php to enable Apache to handle php files. 
The core php packages will then be automatically installed as dependencies.

* Run this command to install three commands at once: 
````
sudo apt install php libapache2-mod-php php-mysql
````
* Run this command to confirm the PHP installation version 
````
php -v
````
````
PHP 7.4.3 (cli) (built: Oct  6 2020 15:47:56) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
````
Now you have a fully functional LAMP STACK which consist of;
* LINUX 
* APACHE 
* MYSQL 
* PHP 
To test your setup with a PHP script, it’s best to set up a proper Apache Virtual Host to hold your website’s files and folders. Virtual host allows you to have multiple websites located on a single machine and users of the websites will not even notice it.

We will configure our first Virtual Host in the next step.
