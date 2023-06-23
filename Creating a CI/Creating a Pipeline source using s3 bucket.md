# AWS S3 BUCKET.
## Amazon S3 or simple storage service is a service that provides object storage through a web service interface. It is highly scalable and reliable. 
This service was used to store the application code that was used for this deployment. A function called versioning was enabled which saves various versions of objects stored.

# HOW TO CREATE AN S3 BUCKET.
* Navigate into AWS Management console  service s3.
* Click the button to create a bucket, name the bucket , click enable versioning.
* Go to permission remove the block all access button and include a policy that allows codepipeline to ‘Get object’ in that bucket.
* Then upload the application code file into the s3 bucket. 

## The following are images of a created s3 bucket named glopipeline, the mage of the uploaded code and the bucket which was publicly accessible.


![Screenshot 2023-05-10 at 01 25 46](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/f8cf1c37-16f0-4e34-bfb6-7c82c5d3bf1f)
![Screenshot 2023-05-10 at 01 25 59](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/f5dd3f83-7108-4d20-83b7-19a2a4bc5729)
![Screenshot 2023-05-14 at 14 01 57](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/65a05cbb-1271-46e4-b640-bd2910aa65c7)
