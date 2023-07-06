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
