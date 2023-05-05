# INSTALLING APACHE AND UPDATING THE WEBSERVER. #
#### Apache is the most widely used webserver software that runs on 67% of all websites in the world.
Apache is a free and open-source software that allows users to deploy their websites on the internet. 
It is fast, reliable, and secure. It can be highly customized to meet the needs of many different environments by using extensions and modules.

Majority of the Word press hosting providers servers use apache as their software servers, 
However, websites and other applications can run on other web server software as well. Such as Nginx, Microsoft’s IIS, etc.

* Run this command to install Apache using Ubuntu package manager 'apt':
````ls
#update a list of packages in package manager
sudo apt update

#run apache2 package installation
sudo apt install apache2
````

* To verify that apache is running in the OS, run the following command:
````ls
sudo systemctl status apache2
````
After running the code the green color indicates that your apahe web server is active in the operating system.

NOTE: Networks distribute traffic through ports endpoints that are configured by the user, it is safe praticse to open 
port only when they are in use to avoid unwanted acces to your data.
Inorder to receive traffic to our Web Server ,the TCP port 80 which is the default port for http  which web browsers use to 
access web pages on the internet needs to be opened. 

In the Ec2 instance the TCP port 22 is opned by deafult after launching the instance which enables access via the SSH,
A rule needs to be added to the EC2 configuration to open inbound connection through port 80:


As we know, we have TCP port 22 open by default on our EC2 machine to access it via SSH, 
so we need to add a rule to EC2 configuration to open inbound connection through port 80: Open inbound port 80

Our server is running and we can access it locally and from the Internet (Source 0.0.0.0/0 indicates ‘from any IP address’).

* Run the following command to ensure that I can exchange data between endpoints from my device to the server : 

```` 
curl http://localhost:80
or
 curl http://127.0.0.1:80
 ````
 
 The above commands does the following:
 they use ‘curl’ command to request our Apache HTTP Server on port 80 
 With the first command we are trying to access our server via DNS name  
 The second command is trying to access it by IP address (in this case IP address 127.0.0.1 corresponds to DNS name ‘localhost’
 and the process of converting a DNS name to IP address is called "resolution"). 
 
 * Run ths command to test the  Apache HTTP server can respond to requests from the Internet. Open a web browser and try to access the following url. 
 ````
 http://<Public-IP-Address>:80
 ````
 * Usin the following command is an alternative to retrieving the Ip address rather than looking it up the AWS Mnagement Console 
 ````
 curl -s http://169.254.169.254/latest/meta-data/public-ipv4
 ````
 Since all web browsers use port 80 by default, the URL in the browser should still function if you do not specify a port number.
 
 Your web server is now correctly installed and reachable over your firewall if you view the following page.

Ubuntu Apache Default Page.
