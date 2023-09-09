# HOW TO CREATE DOCKER IMAGES AND DOCKER FILE SYNTAX
* FROM: Configures the base image as the foundation for a build.

* LABEL: used to add metadata to an image e.g. description or maintainer.
  
* RUN: Run commands in a new layer that can be used for installation or configuration.
  
* COPY: copies the new files or folders from, the source (client machine) to the destination (new image layer)
  
* ADD: does the same thing as copy but you can add from a remote URL and do extraction etc.
  
* CMD: defines the default executable of a container and argument 9e.g.webservers) You can use CMD to state that you want it to run a certain web server or game server. It can be overridden via docker run parameters. It is also the initial process that runs within the container.

* ENTRYPOINT: does the same as CMD but cannot be overridden. It is used when creating single-purpose image.

* EXPOSE: informs docker what port the container is running on.

  This is an example of a docker file.
  ````
  FROM nginx:latest

  LABEL maintainer="gloryanabor1@gmail.com"

  COPY 5000/usr/share/nginx/html

  EXPOSE 80

  CMD ["nginx","-g", "daemon off,"]
  ````
  COPY and save this file in a text editor. This file will be saved in a folder called app1-2048
  
   # BUILDING DOCKER IMAGES FROM A DOCKER FILE.
  Move to the folder where you saved the dockerfile
  
  This Dockerfile uses the latest version of the nginx image (which includes a configured installation of NGINX)

  It sets metadata maintainer. It then copies all of the 5000/ folder from the localdocker host/client machine into the /usr/share/nginx/html folder within the image.

Finally we use the EXPOSE directive to inform uses of this image that the appplication is running on tcp/80 and use the CMD statement to set the initial process for containers running from this image.

To build the image, from the ``app1-2048`` folder we run the docker build command. 
We use ``-t`` to tag the image with 5000 and use . to set the working directory for the command. 
Any paths specified in the dockerfile will use . as the starting point ..the working directory.

* To build run the image run the following command:
``
docker build -t dockerized-2048 .
``
![Screenshot 2023-09-05 at 23 36 32](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/57278472-0685-44f2-8cc3-21d832afca94)


RUNNING A CONTAINER ON 2048 IMAGE
Run the following command to show all images on the Docker Host.
``
docker images
``
![Screenshot 2023-09-05 at 23 37 28](https://github.com/Egal212/DEVOPS-PROJECTS1.0/assets/114033502/1a097094-9a95-4263-b414-0c0f07e3cab6)

Locate the dockerized-5000 image which you just created.

This image, is running an application using ``tcp/80`` so we need to use the ``-p`` 
CLI option to run this on an alternative docker host post.

Run a docker container of 2048 using

``
docker run -d -p 8081:80 dockerized-2048
``



This command will run in detached mode, so your terminal should return to the prompt immediately.

Verify the container is running with ``docker ps``.
Confirm the port mapping with
`` 
docker port <CONTAINERID>.
``
Browse to http://localhost:8081



Cleanup

Run a docker stop <CONTAINERID> to stop the 5000 container app.
Run a docker rm <CONTAINERID> to remove the 5000 container.



 
  
  
