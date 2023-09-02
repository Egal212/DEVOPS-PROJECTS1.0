A tech stack is the set of technologies used to develop an application, including programming languages, frameworks, databases, front-end and back-end tools, and APIs. Examples include;
* LAMP : Linux, Apache, MySql, PHP, Python or Perl.
* LEMP : Linux, Nginix, MySql, PHP, Python or Perl.
* MERN : MongoDB, ExpressJS, ReactJS, NodeJS.
* MEAN : MongoDB, ExpressJS, AngularJS, NodeJS.

Tech Stacks are created depending on the requirement of the web solutions needed. 
In order to create the LEMP websolution , I created a webserver on aws using the UBUNTU 22.4 distribution a with a private key and set incoming traffic to all because it is a sample infrastructure which would not actually be used but for security purpose it is recommended to leave the default port ec2 comes with which is port 22 SSH and provision the required ports only when necessary.

# SSH INTO YOUR EC2 USING THE TERMINAL.
After creating the EC2 web server , i had to ssh into the virtual machine to create the infrasturcture needed for the web solution.
Go to the terminal located in your computer.
* Change directory into the location where your PEM file is. Most likely will be in the Downloads folder.

````
cd ~/Downloads
````
IMPORTANT - Anywhere you see these anchor tags < > ,  it means you will need to replace the content in there with values specific to your situation.
* Change permisions for the private key file (.pem), otherwise you can get an error "Bad permissions"
````
sudo chmod 400 <private-key-name>.pem
````
* Connect to the instance by running.
````
ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>
````
When prompted reply Y and you will be ssh into the server.
