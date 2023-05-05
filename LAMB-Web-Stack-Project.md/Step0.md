
####A webstack is a variety of software that can be used for web development, 
which includes, an operating system(OS), a programming language, databse software,
and a webserver.
There are varieties of stack technologies that make various solutions possible.
These stack of technologies are regarded as WEBSTACK. 

What is a Technology stack? A technology stack is a set of frameworks and tools used to develop a software product.
This set of frameworks and tools are very specifically chosen to work together in creating a well-functioning software. 
They are acronymns for individual technologies used together for a specific technology product. 
some examples include

* LAMP (Linux, Apache, MySQL, PhP)
* LEMP LEMP (Linux, Nginx, MySQL, PHP or Python, or Perl)
* MERN (MongoDB, ExpressJS, ReactJS, NodeJS)
* MEAN (MongoDB, ExpressJS, AngularJS, NodeJS.

The following project documented will be using the **LAMP** Webstack technology,
which is an acroymn for ; LAMP (Linux, Apache, MySQL, PhP).

####Aws is the world's most popular and commonly used cloud network that offers
over 200 fully featured services from datacenters globally.
This project will be executed using the AWS Management console and the CLI.

# LAUNCH AN EC2 INSTANCE #
- Go to the management console, service then Ec2 instance.
- Go to instance create an instance , write the instance name, select the AMI, 
to which i selected ubuntu20.04LTS (HVM)free tier, t2.micro family, created a keypair which was 
download this .pem key pair would be used to ssh into the instance, it should be kept safe 
for security purposes, then you create a security group with inbound rules of http 80 allowing 
0.0.0.0 and ssh allowing 0.0.0.0 this gives http and ssh access to the instance through
those opened ports.

# CONNECTING TO AN EC2 TERMINAL USING MAC/LINUX #
The followung instruction details how to ssh into the instance through the port 22.

* Change the directory to the file where the downloaded PEM file is.
```ls
