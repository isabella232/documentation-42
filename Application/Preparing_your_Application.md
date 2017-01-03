#Preparing Application for Stakater

Since Stakater uses Docker to run applications, it expects each application to have following docker and docker-compose files at its root directory to work.

1. Dockerfile_build
2. Dockerfile_deploy
3. Docker-compose-test.yml
4. Docker-compose-dev.yml
5. Docker-compose-prod.yml


##Writing Dockerfile_build for Application
Used in the docker-compose files,  Dockerfile_build specifies the base image to be used along with specifying which files should be added to the filesystem of the container. The base image is used to create a container which in turn is used to compile, test and build application.
```
# Set the base image to Grails.2.2.4
FROM ahmadiq/grails:2.2.4

# File Author / Maintainer
MAINTAINER Stakater Team

# Create mount point
VOLUME ["/app"]

# Add code to the filesystem of the container
ADD . /app/
```
###Anatomy of Dockerfile_build
`FROM` states the base image to be used when creating the container. In the sample above it’s `ahmadiq/grails:2.2.4` since this sample Dockerfile_build is for a grails application.

`MAINTAINER` (optional) states the value of author field in the generated image. In the sample above it’s Stakater Team.

`VOLUME` instruction creates a mount point with name specified in the instruction. In the sample above /app is the mount point.

`ADD` instruction copies files and adds them to the filesystem of the container. In the sample above, the present working directory (denoted by ‘.’) consisting of all the files in the root directory of application are copied to /app in the container. 

Since the Dockerfile_build is in the root directory, a ’.’ (present working directory) in the Dockerfile would point to the root directory of the application. 


###Restrictions for Dockerfile_build
*  Mapped volume should be `/app`


##Writing Dockefile_deploy for Application
Used to create image for deployment, `Dockerfile_deploy` specifies the base image used for creating the container (like image for tomcat in the sample below) and steps like adding war file and starting tomcat in case of a web application. 
```
# Set base image
FROM codenvy/jdk7_tomcat7

# Add war file
ADD test.war /home/user/tomcat7/webapps/ROOT.war

# start Tomcat
CMD /home/user/tomcat7/bin/catalina.sh run
```




##Writing docker-compose files for test, dev or prod Environments
The sample below shows the content of a docker-compose file. Each environment test, dev and prod will have their own docker-compose file.
```
compile:
  build: .
  dockerfile: Dockerfile_build
  volumes:
    - /app/.grails:/root/.grails
  command: grails refresh-dependencies && grails clean && grails compile -Dgrails.work.dir=/app/.grails

test:
  build: .
  dockerfile: Dockerfile_build
  volumes:
    - /app/.grails:/root/.grails
  command: grails test-app 'unit:' -Dgrails.work.dir=/app/.grails

app:
  build: .
  dockerfile: Dockerfile_build
  volumes:
    - /app/test_app_prod:/app/test_app/outputs/
    - /app/.grails:/root/.grails
  command: grails prod war /app/test_app/outputs/test.war
```


###Anatomy of docker-compose files
There are three services compile, test and app as shown in the sample above.

The command in compile service should compile your application.

The command in test service should run the test cases for your application. If there are no test cases in your application there should still be a test service in docker-compose and provide the compile command again.

The app service should have the command to package your application. If you want to package code for different environments, update the command in app service to specify the environment in each docker-compose file.  For example in the sample above, which is for a grails application, the package command for production environment is 
command: `grails prod war /app/test_app/outputs/test.war`   in `docker-compose-prod.yml` file and
command: `grails test war /app/test_app/outputs/test.war`    in `docker-compose-test.yml`.
 


###Good Practices
Map the directories where application dependencies are downloaded to an external volume. This would speed up the build process as dependencies are downloaded the first time and reused later.


###Restrictions for docker-compose files
There should be three services in the docker-compose, compile, test and app as shown in the sample above.

Package command in app service should specify the output path as `/app/<APP_NAME>/outputs/<PACKAGE_FILE_NAME>`

The outputs directory for the package command should be mapped to `/app/<APP_NAME>_<ENVIRONMENT>` like
```
volumes:
  - /app/test_app_prod:/app/test_app/outputs/
```
in the sample above.
The environment name should be the same as the environment passed in build.

Dockerfile in each service should have the name of the Dockerfile_build in application root directory. If the name for `Dockerfile_build` is changed, change it here in docker-compose files as well.


##Helping Materials:
To learn more about Docker: 
* https://docs.docker.com/
* https://docs.docker.com/engine/reference/builder/
* https://docs.docker.com/compose/reference/

