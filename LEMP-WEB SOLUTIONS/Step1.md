* ## INSTALL NGINX WEB SERVER
In order to install web pages to our site visitors, we are going to install Nginx , a high performance web server. 
We installed that by using the ubuntu package manager ‘apt’
We started off by updated our servers package index, then used apt install to get NGINX installed:
````
sudo apt update
sudo apt install nginx
````
When promoted, enter Y to confirm the installation of Nginx. After the installation, the Nginx web server will be active and running on your ubuntu server.

To verify that nginx was successfully installed and is running as a service in Ubuntu run this code.
````
sudo systemctl status nginx
````
If it shows green and running, then its is running. 

In other to be able to receive traffic into our web server we need to open the port 80 which is the default port that web browsers use to access web pages in the internet.

Port 22 opens by default when using ec2 to access it via ssh, so the inbound rules need to be open for port 80 and 22 sure 0.0.0.0/0 meaning everyone.

To check if we can access it locally in the ubuntu shell run:

````
curl http://localhost:80
or
curl http://127.0.0.1:80
````
![this page, the ngánx web](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/2eee388a-001a-4fb0-bd6d-c29646c85631)

The next step is to test how our Nginx server responds to requests from the internet.
Open a web browser and try to access following url.
````
http://<Public-IP-Address>:80
````
![Screenshot 2023-07-28 at 17 58 27](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/1d9ec77d-0734-4dd0-bec8-1033e52e84d8)


