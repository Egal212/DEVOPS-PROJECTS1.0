* # CONFIGURE MYSQL SERVER TO ALLOW CONNECTTION FROM REMOTE HOST.
Navigate to mysql terminal and run this command.
````
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
````
Replace ‘127.0.0.1’ to ‘0.0.0.0’ like this:

![Screenshot 2023-07-31 at 17 39 05](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/51bef29d-ba49-445c-933a-89a5eeba7ffa)

You can use /bind-address to find it faster.
Note: Bind- address is a way for users to connect to mysql from various networks.

* Restart the service
````
sudo systemctl restart mysql
````
# NAVIGATE BACK INTO THE MYSQL CLIENT SERVER .
In the mysql client server , you will connect remotely to the mysql server without using SSH.
* Run this code
````
sudo mysql -u remote_user -h <input ip addressof mysql server> -p
````
Input the password: Note: The password been asked for is the password whichwas set in for the mysqlserver database.
Here, you will verify that you are connected from the client server by running a few queries.
````
mysql> Show databases;
````
If you can view the test_db you created earlier on the server then the infrasturcture is complete.
