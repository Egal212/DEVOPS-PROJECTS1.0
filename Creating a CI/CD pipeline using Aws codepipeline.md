# PREQUISTIES.
### CI/CD means continous integration and continous delivery. They can be refeered to as the continous devlopement or continous software development.
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
This service was used to store the application code that was used for this deployment. A function called versioning was enabled which saves various versions of objects stored.
# STEPS USED TO CREATE AN S3 BUCKET.
* Navigate into AWS Management console  service s3.
* Click the button to create a bucket, name the bucket , click enable versioning.
* Go to permission remove the block all access button and include a policy that allows codepipeline to ‘Get object’ in that bucket.
* Then upload the application code file into the S3 bucket.
* ELASTIC BEANSTALK: 
* CODE PIPELINE: 
