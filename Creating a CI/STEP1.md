# Creating a pipeline using Aws codepipeline.
### CI/CD means continous integration and continous delivery. They can be referred to as the continous developement or continous software development.
### CI/CD  pipelines is a practice that can be used to  automate the software delivery process in the software development lifecycle.
### CI/CD has become a very important aspect in the world of software development and the way we release new softwares into the world.

# BENEFITS OF CREATING A CI/CD PIPELINE.
* The creation and  distribution of software is faster and easier.
* Getting your software to the world becomes easier.
* The ability for startups to survive depends on the ability to release products at the 
appropriate times.
* It creates a consistent and standardized tooling flow for the development team to work with.
* Improved quality of software, since you can constantly be running test.

## There are four stages that are used to release a software using CI/CD.
* Source: This is the stage where you check in the created code, it could be a java file, python file e.t.c whatever code you used to build your application.You would be inputing through the source.
* Build: At this stage your code might require to be built into an IOS or an Andriod or some type of pacakge. This is also where you can check the style, the performance of your code etc.
* Test: This is the stage where you take your complied code and input it in an enviroment whcih it can be acted upon. This is an enviroment built for thr code that has other system that it can be tested on.This stage could include security testing, penetration testing, or any tested that is related to your application. Generally, you want to confirm your desired fuctionality, catch programming syntax errors to make sure your code doesnt stop running due to this, standardize code patterns and formats,reduce bugs dues to non-desired application usage and logic failure, most importantly make the application make secure.
* Production: Lastly, you want to deploy your code into production, where you can be deploying your code out into a server or an appstore. It is generally a place that can be utilized by your customer.

# AWS TOOLS USED TO CREATE THE PIPELINE.
* S3: Amazon S3 or simple storage service is a service that provides object storage through a web service interface. It is highly scalable and reliable. 
* ELASTIC BEANSTALK: The code will need a target environment containing virtual servers, or amazon ec2 instances, before it can be deployed. This environment was prepared using the elastic beanstalk.
Elastic beanstalk is a platform as service that creates an environment that you can use to deploy your code with everything the code needs built into it. It provides capacity provisioning, autoscaling, load balancing.
* CODE PIPELINE: AWS Codepipeline is a continuous delivery service that can be used for fast and reliable application updates.

