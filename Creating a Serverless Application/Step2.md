The previous stage detailed the configuration of the simple email service SES. This stage explains how to extend and add lambda and some configuration to allow our state machine to use the simple email service.
At this stage we will be creating a lambda function and configuring the permissions so that the lambda function can utilise the SES to send us notification emails.
Although, in irder to do this we will need to create a lambda execution role which is what gives the lambda function the permission it needs to interact with SES.

# CREATING AN IAM ROLE.
In this stage, i created an iam role which the email lambda function will use to interact with other aws services.
This iam role can be created manually but for speed and reusuability , this will be created using this cloudformation template.
Click https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://learn-cantrill-labs.s3.amazonaws.com/aws-serverless-pet-cuddle-o-tron/lambdarolecfn.yaml&stackName=LAMBDAROLE
Tick the I acknowledge that AWS Cloudformation might create IAM resources box and then click CREATE STACK.

Confirm that the stack is showing a CREATE COMPLETE state before moving into the next.


Navigate into the IAM Console and review the execution role. You will notice that the role provides SES,SNS and logging permissions to whatever assumes the role. This IAM permission is what gives lambda ther permission to interact with those services.
![Screenshot 2023-06-29 at 12 54 20](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/70a6ba2d-6a21-4111-92cb-03b0368618a3)

# CREATING A LAMBDA EXECUTION ROLE.
This lambda execution role is a function which will be used by the serverless application to create an email and then send it using SES.
Navigate to lambda on the aws management console.
Click on Create Function
Select Author from Scratch
For function name enter email_reminder_lambda (or any other name of choice)
and for runtime click the drpdown and pick Python 3.9
Expand Change default execution role
Pick to Use an existing role 
Click the Existing Role dropdown and pick LambdaRole 
Click Create Function.

# CONGIGURE THE email_reminder_lambda function.


