In this step the state machine needs to be added to the infrastructure which is the main component of the serverless application.

The state machine is what manages the flow of the application. it will initially pause for a number of seconds, the time until the next requirements, after the time is expired the state machine now uses the email lambda function that was previously created to send the notifictaion to the customer or target emails.

This is an end-to-end serverless application where the state machine waits a certain amount of time and uses a Lambda function and the simple email service to send an email notification.


# CREATING A STATE MACHINE ROLE
A state machine role needs to be created for the state machine to have the permission to interact with other AWS services.
This can be created manually but, this was created using the cloud formation link.
Click https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/quickcreate?templateURL=https://learn-cantrill-labs.s3.amazonaws.com/aws-serverless-pet-cuddle-o-tron/statemachinerole.yaml&stackName=StateMachineRole
Check the ``I acknowledge that AWS CloudFormation might create IAM resources.`` box and then click ``Create Stack``

Wait for the stack to move into the ``Create_Complete`` state before moving into the next.
Verify the role on the iam console the role should look like this.
![Screenshot 2023-06-29 at 13 50 08](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/cdbedd06-4dda-436c-8b35-c0ee7793f647)

The role was given the logging permisiions, the ability to invoke the email lambda function when it needs to sed emails, the ability to use SNS to send text messages.

# CREATE THE STATE MACHINE.
Navigate to the AWS Step Function Console
Click the ``Hmaburger Menu`` at the top left and click the ``StateMachine``
Click ``Create state Machine``
Select ``Write your workflow in code`` which will allow you to use Amazon States Language
Scroll down for ``type`` select ``standard``
Download and paste this into the clipboard: https://learn-cantrill-labs.s3.amazonaws.com/aws-serverless-pet-cuddle-o-tron/pet-cuddle-o-tron.json

Note: This code is the Amazon State Language (ASL) file for the state machine.
State machines can be defined using ASL , (Amazon States Language) which means if you already have the all of a state machine you can use that to directly create the state machine, rather than having to code it manually.

The state machine starts and then wiats for a certain time period based on the ``Timer`` state. This is controlled by the web front end that will soon be deployed, then the email is used which sends an email reminder.

What this code details is you start at the start point and then move on to the state called timer. A timer is a wait state , this essentially just waits for a certain number of seconds, and the number of seconds to wait is provided into the state machine as an input.The timer waits until that number of seconds expires and it could be any time inputted,days, weeks, etc. It then moves on until the next state which is the email state. 
The email state is the task state, this performs a task and then moves onto the next state.
Currently the task indicates that it invokes the lambda function.

We give it the lambda function to execute using the function name parameter and this accepts an ARN of a lambda function. It invokes this lambda function and it provides a payload and the payload is the input to this stage machine.
So it is giving all the input the state machine receives and its putting that through to the email lambda functions. So this is how the lambda function gets the information that it needs, which in this case is the email address to send the email reminder to

Once this lambda function has finished invoking it then moves on to the next state, which is also called next state which is of type pass , end or true. And that finishes the execution of the state machine.

A state machine can also easily use express or standard mode. Where standard has the maximum execution time of one year whereas express was designed for event-driven workflows, for streaming data, micro services not, mobile backends, or other short-duration high transaction rate workloads.

You will need to change the state machine name to a name of choice, choice an existing role, scroll down and change the logging from off to all , this will allow the state machine to log its execution details into cloud watch logs and if we have any problem can troubleshoot with the data.

Then Click ``Create State Machine``
Copy down the ARN of the state machine.

![Screenshot 2023-06-29 at 21 01 26](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/7f21f0a1-5ece-48b5-8761-a9e2d934a1c5)


# CONFIGURE THE STATE MACHINE
In this state machine ASL which is the code locate the ``Emailonly`` definition. Look for the``Email_Lambda_ARN`` which is a placeholder anf replace with the email_reminder_lambda arn. 

![Screenshot 2023-06-29 at 20 52 42](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/80cb8083-ae6e-4253-9c2f-bb21f464d5ec)


Scroll down to the bottom and Click ``next`` For ``State machine name`` use the name of choice.
Scroll down and under ``Permisiions`` select ``Choose an existing role`` and select ``StateMachineRole`` from the dropdown.
SCroll down to ``Logging``, change the ``LogLevel`` to ``ALL``
Scroll down to the bottom and click ``Create State Machine``
Locate the ARN of the state machine and note it down.

![Screenshot 2023-06-29 at 21 01 38](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/a2443502-5e73-4065-8b37-37eb24e5288d)



#FINISH
At this stage ypu have configired the state machine which is the cire part of the serverless application.
The state machine controls the flow through the pplication and is responsible for interacting with other AWS services.



