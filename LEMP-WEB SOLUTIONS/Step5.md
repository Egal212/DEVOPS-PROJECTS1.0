* # TESTING PHP WITH NGINX
Testing PHP with nginx
Your LEMP stack should now be completely set up.

At this point, your LAMP stack is completely installed and fully operational.
You can test it to validate that Nginx can correctly hand .php files off to your PHP processor.

You can do this by creating a test PHP file in your document root. Open a new file called info.php within your document root in your text editor:

````
sudo nano /var/www/projectLEMP/info.php
````
Type or paste the following lines into the new file. This is valid PHP code that will return information about your server:
````
<?php phpinfo();
````
Save the file and exit the text editor (Ctrl + O, Enter, Ctrl + X for nano).

You can now access this page in your web browser by visiting the domain name or public IP address you’ve set up in your Nginx configuration file, followed by /info.php:

````
http://`server_domain_or_IP`/info.php
````
Replace ‘server_domain’ with your public IP address.
You will see your server page containing detailed information about your server.


![Screenshot 2023-07-28 at 19 34 02](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/f0520897-5c69-48d6-899c-f2bae13c9926)

After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment and your Ubuntu server. You can use rm to remove that file:
````
sudo rm /var/www/your_domain/info.php
````
Replace your domain with ur domain name file u created in this case projectLEMP.

You can always regenerate this file if you need it later.
