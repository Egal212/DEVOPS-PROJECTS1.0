* Update and Install the Mysql into the server.
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
    
  * Update and Install mysql
      ````
      sudo apt update -y
      ````
      Navigate to the AWS Management Console to the mysql server , go to the security group and edit the inbound rule to Type: Mysql/Aurora, Port: TcP, PortRange : 3306 and save rule. This is opening the port for mysql.

    
      
