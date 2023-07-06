At this stage we will be adding  the client side application . The application will be delivered from an s3 bucket using static hosting. 

So we are going to create an s3 bucket, set it as publicly accessible , configure it as a static website and then edit the client application files to post at your specific installation of this serverless application using the address of the API Gateway that was created. 
Then we upload all the files and test that the application functions.

# CREATE THE S3 BUCKET
Navigate to ``s3`` on the console
Click ``Create bucket``: name the bucket 
Untick the ``block all public access`` on bucket and tick the ``I acknowledge that the current settings might result in this bucket and the object becoming public``.
Scroll down to the bottom and click ``Create bucket``

![Screenshot 2023-07-06 at 21 46 50](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/3d9759cc-14c6-42dd-b00c-88adb4aba7f7)




# CONFIGURE THE BUCKET AS PUBLIC
Navigate to the bucket name and click
Go to ``permissions`` tab
Scroll down and in the ``Bucket Policy`` area, click ``edit``.
In the box paste this code below;
``
{
    "Version":"2012-10-17",
    "Statement":[
      {
        "Sid":"PublicRead",
        "Effect":"Allow",
        "Principal": "*",
        "Action":["s3:GetObject"],
        "Resource":["REPLACE ME ARN/*"]
      }
    ]
  }
  ``
Replace the REPLACE ME ARN without removing the /* with the bucket ARN.
Click ``Saves Changes``

![Screenshot 2023-07-06 at 21 46 40](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/e4b14eb4-0263-4ed0-bc29-6ca3ee292f5f)

Paste this code on the policy
# ENABLE STATIC HOSTING
Next you need to enable static hosting on the s3 bucket so that it can be used asa front end website.
Click on the ``Properties Tab``
Scroll down and locate ``Static website hosting``
Click ``Edit``
Select ``Enable`` Select ``HOST A STATIC WEBSITE`` 
For both ``Index Document`` and ``Error dOCUMENT`` enter ``index.html`` Click ``Save Changes``
Scroll down and locate ``Static website hosting`` again.
Under ``Bucket Website Endpoint`` copy nad noe down the bucket encryption URL.

# DOWNLOAD AND EDIT THE FRONTEND FILES.
Download and unzip the file https://learn-cantrill-labs.s3.amazonaws.com/aws-serverless-pet-cuddle-o-tron/serverless_frontend.zip
Within this file is the frontend html and jvascript that needs to beedited and uploaded into the s3 bucket.

Open the ``serverless.js`` in a code/text editor. Locate the placeholder ``REPLACEME_API_GATEWAY_INVOKE_URL`` . replace it with your API Gateway Invoke URL at the end of this URL.. add ``/petcuddleotron`` it should look something like this ``https://somethingsomething.execute-api.us-east-1.amazonaws.com/prod/petcuddleotron`` Save the file.

![Screenshot 2023-07-06 at 21 46 29](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/6a25aa33-f160-4567-b139-3a117fb907e2)



# UPLOAD AND TEST THE INFRASTRUCTURE
Return to the S3 console Click on the ``Objects`` Tab.
Click ``Upload``
Drag the 4 files from the serverless_frontend folder onto this tab, including the serverless.js file you just edited. MAKE SURE ITS THE EDITED VERSION

Click ``Upload`` and wait for it to complete.
Click ``Exit``
Verify All 4 files are in the ``Objects`` area of the bucket.

![Screenshot 2023-07-06 at 21 46 29](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/e8f6edb9-7189-4f2a-9b9f-d93d8856a09e)



Open the ``PetCuddleOTron URL`` you just noted down in a new tab.
What you are seeing is a simple HTML web page created by the HTML file itself and the ``main.css`` stylesheet. When you click buttons .. that calls the ``.js`` file which is the starting point for the serverless application.

![Screenshot 2023-07-03 at 20 31 37](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/45b52546-1e64-458c-88a5-679a6350cb57)


Ok to test the application Enter an amount of time until the next cuddle ...I suggest ``120`` seconds Enter a message, i suggest ``HUMAN COME HOME NOW``
then enter the ``PetCuddleOTron Customer Address`` in the email box, this is the email which you verified right at the start as the customer for this application.

before you do the next step and click the button on the application, if you want to see how the application works do the following open a new tab to the ``Step functions console`` https://console.aws.amazon.com/states/home?region=us-east-1#/statemachines
Click on ``PetCuddleOTron``
Click on the ``Logging tab``, you will see no logs CLick on the ``Executions`` tab, you will see no executions..

Move back to the web application tab (s3 bucket)
then click on ``Email Minion`` Button to send an email.


Got back to the Step functions console make sure the ``Executions`` Tab is selected click the ``Refresh`` Icon Click the ``execution``
Watch the graphic .. see how the ``Timer state`` is highlighted The step function is now executing and it has its own state ... its a serverless flow. Keep waiting, and after 120 seconds the visual will update showing the flow through the state machine

![Screenshot 2023-07-03 at 20 36 35](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/69b68bb3-43a0-4032-aeb8-361104972f12)


Timer .. waits 120 seconds
``Email`` invokes the lambda function to send an email
``NextState`` in then moved through, then finally ``END``
Scroll to the top, click ``ExeuctionInput`` and you can see the information entered on the webpage. This was send it, via the ``JS`` running in browser, to the API gateway, to the ``api_lambda`` then through to the ``statemachine``

![Screenshot 2023-07-04 at 15 26 11](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/7e3411e0-27db-4e79-ade7-75034a7aaa07)


Click ``PetCuddleOTron`` at the top of the page
Click on the ``Logging`` Tab
Because the roles you created had ``CWLogs`` permissions the state machine is able to log to CWLogs Review the logs and ensure you are happy with the flow.
![Screenshot 2023-07-04 at 15 37 51](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/ec3c45ee-992e-4293-8273-ef97b963d5f8)


![Screenshot 2023-07-04 at 15 38 09](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/5f55ac60-a7bf-40a2-9e76-9fcc216c70e7)

![Screenshot 2023-07-03 at 20 35 21](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/4db18c8f-b54f-4321-a874-8361e1c3876f)







# FINISH
At this point thats everything .. you now have a fully functional serverless application

* Loads HTML & JS From S3 & Static hosting
* Communicates via JS to API Gateway
* uses api_lambda as backing resource
* runs a statemachine passing in parameters
* state machine sends email
* state machine terminates
* No servers were harmed, or used even, in this production 



