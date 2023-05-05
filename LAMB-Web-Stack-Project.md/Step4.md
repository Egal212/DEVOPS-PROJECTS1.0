#CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE#
Apache is a web server that needs some information to display contents to your website.
These informations are placed in the virtual host.

In this stage u will be setting up a domain named projectlampwebstack1.  
Apache or ubuntu has a default server block  that has been configured to serve documents from /var/www/html directory.

I will be leaving this default host as it is and be adding another directory beside it.

* Create a directory for projectlampwebstack1 

````
sudo mkdir /var/www/projectlampwebstack1
````
Because u created the directory with the root, only the root has access , which gives less access inorder to create access u change the ownership.
* The following command assign ownership of the directory with your current system user:
````
sudo chown -R $USER:$USER /var/www/projectlampwebstack1
````
* This uses the $user variable to change the user away from root to ubuntu .

* create the configuration file for the web server using vim.
````
sudo vi /etc/apache2/sites-available/projectlamp.conf
````
This code opens a blank file in vim which you will use to create the configuration file
````
<VirtualHost *:80>
    ServerName projectlampwebstack1    ServerAlias www.projectlampwebstack1
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlampwebstack1
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
````
To save and close the file, simply follow the steps below:

Hit the esc button on the keyboard
Type :wq. w for write and q for quit
Hit ENTER to save the file

* Check the site available directory with this command.
````
sudo ls /etc/apache2/sites-available
````
You will view the following output:
````
000-default.conf  default-ssl.conf  projectlamp.conf
````
With this VirtualHost configuration, we’re telling Apache to serve projectlamp using /var/www/projectlampwebstack1 as its web root directory.
If you would like to test Apache without a domain name, 
you can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. 
Adding the # character there will tell the program to skip processing the instructions on those lines.

* Run this command to use a2ensite to enable the new virtual host:
````
sudo a2ensite projectlampwebstack1
````
You might want to disable the default website that comes installed with Apache. 
This is required if you’re not using a custom domain name, because in this case Apache’s default configuration would overwrite your virtual host. 
To disable Apache’s default website use a2dissite command , type:
````
sudo a2dissite 000-default
````
* This command ensures your configuration file doesn't contain syntax erros.
````
sudo apache2ctl configtest
````
Finally, reload Apache so these changes take effect:
````
sudo systemctl reload apache2
````
Your new website is now active, but the web root /var/www/projectlamp is still empty.
Create an index.html file in that location so that we can test that the virtual host works as expected:
````
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' 
$(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
````
Now go to your browser and try to open your website URL using IP address:
````
http://<Public-IP-Address>:80
````
If you see the text from ‘echo’ command you wrote to index.html file, then it means your Apache virtual host is working as expected. 
In the output you will see your server’s public hostname (DNS name) and public IP address. 
You can also access your website in your browser by public DNS name, not only by IP – try it out, 
````
http://<Public-DNS-Name>:80
````
You can leave this file in place as a temporary landing page for your application until you set up an index.php file to replace it. 
Once you do that, remember to remove or rename the index.html file from your document root, as it would take precedence over an index.php file by default.
the result must be the same (port is optional)
