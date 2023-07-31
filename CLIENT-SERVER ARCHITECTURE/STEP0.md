
* # CLIENT - SERVER ARCHITECTURE.
  A client-server architecture refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.

  # IMPLEMENTING A CLIENT-SERVER ARCHITECTURE BY USING MYSQL DATABASE MANAGEMENT SYSTEMS. (DBMS)
  * Launch and Configure two Linux-based Virtual server EC2 instanes in AWS Using the Ubuntu Distribution.
  * Names
    ````
    Server name A -Mysql Client.
    Server name B -Mysql Server.
    ````

# SSH INTO THE MYSQL SERVER FROM THE TERMINAL MAC/WINDOWS.
After creating the EC2 web server , ssh into the virtual machine to create the infrasturcture needed for the web solution. Go to the terminal located in your computer.

Change directory into the location where your PEM file is. Most likely will be in the Downloads folder.
````
cd ~/Downloads
````
IMPORTANT - Anywhere you see these anchor tags < > , it means you will need to replace the content in there with values specific to your situation.

Change permisions for the private key file (.pem), otherwise you can get an error "Bad permissions"
````
sudo chmod 400 <private-key-name>.pem
````
Connect to the instance by running.
````
ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>
````
When prompted reply Y and you will be ssh into the server.
