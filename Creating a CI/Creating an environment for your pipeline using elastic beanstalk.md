# HOW TO CREATE A PIPEPLINE ENVIRONMENT USING ELASTIC BEANSTALK.
#### The code will need a target environment containing virtual servers, or amazon ec2 instances, before it can be deployed. This environment was prepared using the elastic beanstalk.
Elastic beanstalk is a platform as service that creates an environment that you can use to deploy your code with everything the code needs built into it. It provides capacity provisioning, autoscaling, load balancing.
# Using the AWS Mangement Console.
* Navigate to the elastic beanstalk.
* Create a new application from the left side bar and give the application a name.


![Screenshot 2023-05-15 at 03 24 09](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/65ed4223-a99d-47cf-b7c2-af4564747cf3)

### Amazon elastic beanstalk has tw0 types of enviroment the webserver environments and the worker environments.
* Select the web server environment.
![Screenshot 2023-05-15 at 03 24 46](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/546edcae-c763-4a49-b736-f48a950bf21d)

* Using Elastic beanstalk you can either configure an already exisiting tech stack that is already launched or you can select the tech stack you will like to use in your enviroment. I selected the tech stack that i would like elastic beanstalk to provision for me.
![Screenshot 2023-05-15 at 03 25 38](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/cec9924f-d742-4ea4-a3b2-7e7791300d2e)

* You will need to create or use an exiting service role that will provide your envionment the necessary access and permissions needed for your ec2 and the ec2key pair you will like to use in order to ssh into the ec2 instance that elastic beanstalk will provison for you.
![Screenshot 2023-05-15 at 03 26 09](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/edfb747b-9b63-488d-b4a7-8845f3548034)

* Depending on what you will like to include in your enviornmentat this next stage you can set up all the necessary details.
* ![Screenshot 2023-05-15 at 03 26 27](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/69ed128c-0e12-4b21-9fd0-85fb3dcb1cd0)

* AFter setting up your environmanets click next and ensure you have either configured or setup the desired tech stack then you create an environment.

![Screenshot 2023-05-15 at 03 27 44](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/6850467c-3b5c-4dde-8915-73b22190a038)
![Screenshot 2023-05-15 at 03 30 38](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/0222e68e-14e5-4622-b63e-e388c3613ef9)

* After creating the enviornment if successful the you will see an envronemnt with a healthy status.
![Screenshot 2023-05-15 at 03 31 17](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/b0ad7ffc-e0df-41bf-ba04-4cb72954060e)
