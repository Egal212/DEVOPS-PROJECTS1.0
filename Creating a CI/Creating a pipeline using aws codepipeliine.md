# CREATING A PIPELINE USING AWS CODEPIPELINE .
### AWS Codepipeline is a continuous delivery service that can be used for fast and reliable application updates.
* Builds, test and deploys your code every time  there is a code change.
* Integrates with a number of third party tools and AWS services.
## The AWS Codepipeline is a great tool used to create a pipeline used to release and update software, this can be done by selecting the source, build and test stage using aws code build, and deploying it using the deployemet parameters configured into it.
## It is also a great tool because it is cheap and if there something wrong with your code, it can easily be troubleshooted.

# HOW TO CREATE A PIPELINE USING THE AWS MANAGEMENT CONSOLE.
* Navigate into the management console and go to the codepipeline.
* The left sidebar click create a pipeline and chhose the piepline settings.
* ![Screenshot 2023-05-14 at 15 01 49](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/8ee87670-3c94-4042-ad3e-8393e0823ceb)
The you select the source, the code build stage if you have one configured in either docker or etc and the deployment environement and deploy your pipeline.
* Add a source stage 

![Screenshot 2023-05-14 at 15 01 58](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/8ab072de-10ed-4c09-a038-148c334090f2)
 ### I added my source stage using the aws s3 bucket i created earlier for the pipeline in which i uploaded my appliation code.
 * Next you have the option to test and build your application using code build but i skipped this stage because my code wasnt dynamic enough to be built .
 * Deploying the application code
 * the application code was deployed using the elastic beanstalk environment i created earlier, i selcted the region i would like this application to be deployed into, the application name and the environment name.
 ![Screenshot 2023-05-14 at 15 02 34](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/f2ce471d-c96b-4587-892b-132e2f85e1c6)

### You can create the pieplie after confirming that paramteres included is accurate.
![Screenshot 2023-05-14 at 15 02 48](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/bad388ae-cd5f-423a-ac5d-82ba7f6b8668)

* Click create pipeline and the pipeline will be created and deployed.


![Screenshot 2023-05-14 at 14 50 08](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/17f7dc3b-d619-45f2-8159-fc15f454c0ad)
