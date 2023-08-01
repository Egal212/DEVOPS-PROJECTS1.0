# GO TO THE WEBSERVER INSTANCE
1. UPDATE THE INSTANCE. 
Note: Updating redhat takes some time.
````
sudo yum -y update.
````
* Verify the security groups.
Note: Redhat needs the lastest configurations of PHP)

2. Install wget, Apache and it’s dependencies
 ````
sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json
````
Installing EPEL REPOSITORY
````
sudo dnf install https:// dl.fedora project.org/pub/epel/epel-release-latest-8.noarch.rpm
````
Note: Epel repository is like a store that manages the kimd of software available to redhat eg php.
Install remi-repository
In the remi-repository we have the yum utils, we install both repos to have a complete basket.
````
sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm-v
````
To display the avaialblle php versions 
````
sudo dnf module list PHP
````
Note: Wordpress is a content managemtn system but based in PHP, so we need the latest version of PHP for it to work woth it.
In order to install the latest version of PHP, we need to reset the PHP modules.
````
sudo dnf module reset php
````
When prompted reply:y 
To enable PHP:
````
sudo dnf module enable php: <input the latest version>
````
To install php run:
````
sudo dnf install php -opache
php-gd php-curl php-mysqlnd
````
Check the version installed and compare it to the latest.
````
php -v
````
Run the following command to run ,enable and check status php
````
sudo systemctl start php-fpm
sudo systemctl enable php-fpm
sudo systemctl status php-fpm
````
Note: Because Centos has advanced security policies we need to set policies that gives certain permisiions .
To instruct the SElinux to allow apache to execute PHP code via PHP-FPM run:
````
setsebol -P httpd_execmem 1
````

start and check status Apache
````
sudo systemctl start httpd
sudo systemctl status httpd
````
RUN:
````
sudo ls -l
````
Copy the public ip address of the webserver , paste it in the browser to verify the apache/redhat works.

Steps to download wordpress on the webserver.
Download wordpress and copy wordpress to var/www/html
````
mkdir wordpress
  cd   wordpress
  sudo wget http://wordpress.org/latest.tar.gz
````
Note: This code downloads wordpress into the wordpress dir, extracts and configures it and then copies it into over to /var/www/html
Verify:
````
ls -l
````
To extract the wordpress run:
````
sudo tar xzvf latest.tar.gz
````
AFter extraction we get an extra folder called wordpress.
Use ``ls -l`` to view it.
Run
````
cd wordpress
ls -l
````
Create the wp-config.php file and copy wp-config-sample into it using.
````
sudo cp -R wp-config-sample.php wp-config.php
````
Use ``ls -l`` to view it.
Run ``pwd`` you should be in 
````
wordpress/wordpress
````
Run ``cd..``
``ls``
You should output
``latest.tar.gz  wordpress``
Copy wordpress to /var/www/html
````
sudo cp -R wordpress/ /var/www/html/
cd /var/www/html
ls -l (confirmt the wordpress)
````

RUN;
````
sudo rm -rf wordpress/
sudo rm  -rf lost+fond/
cd ../..
cd
ls
cd wordpress
ls
ls -l wordpress
````

To open the wordpress folder and copy the content
````
sudo cp -R wordpress/. /var/www/html/
sudo ls -l /var/www/html
cd /var/www/html
ls
sudo yum install mysql-server
````
Note: You are downloaidng mysql-server because the weberver will be acting as a client.
Wordpress has its own database and needs a database server to store login details etc. which is what we just downloaded.



