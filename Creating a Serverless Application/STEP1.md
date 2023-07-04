# CREATING A SERVERLESS APPLICATION.
 This project details the implementation of a serverless reminder application.The application loads from an s3 bucket and runs in the browser which communicates using AWS Lambda and step function via an API Gateway Endpoint. With this application you will be able to configure reminders that will be sent through emails.

# VERIFYING THE EMAIL ADDRESSES USING AWS SIMPLE EMAIL SERVICE (SES).
 The aws ses service is a managed service that lets you send emails to a target list. When fully enabled it allows you to send and receive emails within your application. However, to avoid spam it begins in a sandbox mode which means that the emails addresses used for the application has tobe verified. The serverless application is going to send reminder messages via email using the SES in the sandbox mode.



# CREATING AN EMAIL NOTIFICATION LIST USING SES.
 Login into the aws management console, set the region you would like to use and ensure that the account has admin priviledges.
 Navigate into the SES console,
 Click on Verified Identitites under Configuration.
 Click Create Identity.
 Tick the 'Email Address' Checkbox.
 There were two different email added to the SES that was used for this application. One email address were the application was sent from and the other email were it was sent to.

 Enter the email you would like to send the reminder emails FROM. I will be using gloryanabor1@gmail.com.
 Click Create Identity.
 
![Screenshot 2023-06-29 at 12 13 13](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/1a506c43-84c5-4519-a6df-570e810faa12)

 

 You will then receive a link in the from email inputed to verify the email. 
 After verifying refresh the SES console and it the email will indicate verified. 
REPEAT the same process for the remaining emails you will like to send the notification emails to.

At this stage you have successfully added either one or two verified identities to the simple email address which will allow the serverless application that you are going to implement to use these addresses to send emails.

![Screenshot 2023-07-04 at 17 15 05](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/894a21e8-406e-4658-971a-e20f6a02568a)

