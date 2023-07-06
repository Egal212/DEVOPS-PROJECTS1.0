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

 # CONFIGURE THE LAMBDA FUNCTION 
 Scroll down and remive all the coe from the lambda_function text box. Open this link in a new tab https://learn-cantrill-labs.s3.amazonaws.com/aws-serverless-pet-cuddle-o-tron/api_lambda.py and copy it to your clipboard.
 Select the existing lambda code and delete it.
 Paste the code into the lambda function.

 This is the function which will compute to API Gateway.
 For the code pasted in the link above, you need to locate the ``YOUR_STATEMACHINE_ARN`` placeholder and replace this with the State Machine ARN you noted down in the previous step.
 Click ``Deploy`` to save the lambda function and configuration.

 # CREATE API
 
