In this step we will be creating the lambda function that supports the API gateway and the API gateway itself which will function as the entry point of the application.
* This stage will be adding the APIgateway and the lambda function. This will create n endpoint that my client application canuse to talk to our application.
* We will also be creating an API itself, a method on that API which is how the client application can interact with that API.
* We will also be creating a lambda function which will provide the compute required to service that API.
 Generally, this means that when the client application connects into the API Gateway using the method, the lambda function will be invoked and it will perform actions, but the only billing will be for the compute time that's used as part of the event driven architecture.

# CREATING API LAMBDA FUNCTION THAT SUPPORTS API GATEWAY
Navigate to the lambda console in the AWS management console.
Click on ``Create Function``
for ``Function Name`` Use ``api_lambda``
for ``Runtime`` use ``Python 3.9``
Expand ``Change default execution role``
Select ``Use an existing role``
Choose the ``LambdaRole`` from the dropdown
Click ``Create Function``
 This is the lambda function that will support the Api Gateway.
![Screenshot 2023-06-29 at 21 19 03](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/269a0025-540b-4517-a5f3-2fa8ea9f4c2d)

 

 # CONFIGURE THE LAMBDA FUNCTION 
 Scroll down and remove all the code from the lambda_function text box. Open this link in a new tab https://learn-cantrill-labs.s3.amazonaws.com/aws-serverless-pet-cuddle-o-tron/api_lambda.py and copy it to your clipboard.
 Select the existing lambda code and delete it.
 Paste the code into the lambda function.

 This is the function which will compute to API Gateway.
 For the code pasted in the link above, you need to locate the ``YOUR_STATEMACHINE_ARN`` placeholder and replace this with the State Machine ARN you noted down in the previous step.
 Click ``Deploy`` to save the lambda function and configuration.

 ![Screenshot 2023-07-06 at 20 07 54](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/d77d7768-8e60-45a8-9668-2356b802c5bc)


 # CREATE API
 The api lambda function has been created, the next step is to create the api Gateway, API and Method which the frontend  of the serverless application will communicate with. 
 Navigate to API Gateway on the  management console , 
 Click ``APIs`` on the menu on the left
 Locate the ``REST API`` box, and click ``Build``. if you see a pop-up dialogue ``Create new API`` ensure ``New API`` is selected.

 For ``Api name`` name your api
 FOr ``Endpoint Type`` pick ``Regional`` Click ``create API``

 ![Screenshot 2023-06-29 at 23 52 57](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/86d16fa4-c5c3-4f80-8154-8051cce1687c)


 # CREATE RESOURCE
 Click the ``Actions`` dropdown and Click ``Create Resource``
 Under resource name enter the name 
 Make sure that ``Configure as proxy resource`` is Not ticked- this forwards everything as is , through a lambda function, because we wnt some control, we DONT want this ticked.
Towards the bottom , ensure to tick ``Enable API Gateway CORS``
This relaxes the restrictions on things calling on ut API with a different DNS name, it allows the code loaded from the s3 bucket to call the gateway endpoint. if you DONT check this box, the API will fail.
Click ``Create Resource``

![Screenshot 2023-06-30 at 00 06 17](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/afa3360a-72d2-4625-87fe-67d5a181c626)


# CREATE METHOD
After creating the resource , we create the method , this is the actual point that our client application will directly communicate with .
Click on ``actions`` ; ``create method``.
Click ``post`` in the dropdown and click on the tick icon next to it.
This is configuring the method to be a post type. So when our client application interacts, its going to use the post method of interacting with this particular part of the API Gateway.

![Screenshot 2023-06-30 at 00 08 28](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/7e995a2d-f718-4a26-bdfd-97412c400bea)



Ensure the ``Integration Type`` that ``Lambda Function`` is selected.
Make the region is selected for the Lambda Region
In the Lambda Function box, start typing ``api_lambda`` and it should autocomplete, click this auto complete (Ensure you pick api_lambda and not email reminder lambda).

Ensure that ``Use Default Timeout`` box is ticked.
Ensure that ``Use Lambda Proxy Integration`` box is ticked, this make sure that all of the information provided to this Api is sent on to lambda for processing in the ``event`` data structure.
If you dont tick this box the API will fail.
Click ``Save``
You may see a dialogue stating ``You are about to give API Gateway permission to invoke your Lambd function:. This means aws is requesting confirmation to adjust the ``resource policy`` on the lambda function toallow API gateway to invoke it. 

# DEPLOY API
Now the API,Resource and Method are configures- you now need to deploy the API out to API gateway, specifically an API Gateway stage.
Click ``Actions`` Dropdown and ``Deploy API``
For ``Deployment Stage`` select ``New Stage``
For stage name and stage description enter ``prod``
Click ``DEPLOY``


![Screenshot 2023-06-30 at 00 13 18](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/33fd4c4f-fbb4-416e-98e9-6d3ec32db432)



At the top of the screen will be an ``invoke Url`` note this down somewhere safe, you will need it in the Next Stage.



at this stage yu have configured 
* SES
* An email Lambda function to send email using SES.
* A state machine configured which can send email after a certain time period when invoked.
* An API, resource and method , which can use a lambda function for backing deployed api out to the prod stage of the APi gateway.
  



 
 
