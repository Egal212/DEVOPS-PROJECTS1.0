* Update and Install the Mysql into the server software.
  ````
  sudo apt update -y
  sudo apt install mysql-server -y
  ````
* Enable the Service.
    ````
    sudo systemctl enable mysql
    ````
* Navigate into the Mysql-client server and ssh into it.
    Repeat the ssh process from step0.md
    
  * Update and Install mysql client software.
      ````
      sudo apt update -y
      ````
By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

Navigate to the AWS Management Console to the mysql server , go to the security group and edit the inbound rule to Type: Mysql/Aurora, Port: TcP, PortRange : 3306, Source: < Input the Ip address of the mysql client >  and save rule. 
You can get the ip address from the managment console or by typing 
````
ip addr show
````
on the mysql client terminal.
The ip address is located under 2: on the 3rd line copy the inet < ip address> 

Install and run the following security script on mysql server terminal.
````
sudo mysql_secure_installation
````
Note: 
I would like to use a simple password for this databae , i wont be using the validate password setup but for corporations it is recommended to click Y.
Click No
* Then i set a password for root.
* Repeat y to every other questions.

````
mysql> sudo mysql
````
* Create a user on mysql.
````
mysql> CREATE USER 'remote_user'@'%' IDENTIFIED WITH mysql_native_password BY '<add password>';
````
* Create a database
````
mysql> CREATE DATABASE test_db;
````
* Grant Priviledges
````
mysql> GRANT ALL ON test_db .* TO 'remote_user'@'%' WITH GRANT OPTION;
````
````
mysql> FLUSH PRIVILEGES;
````
````
mysql> exit;
````
      
