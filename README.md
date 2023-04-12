DEVOPS REAL TIME CI PROJECT

In this project, I created an end-to-end CI pipeline while keeping in mind devops principal and used all these tools Git, GitHub , Jenkins,Maven,, SonarQube, Docker, AWS , Docker Hub, nexus repo  to achive the goal.

Project Architecture:

<img width="4328" alt="TERAAFORM PROJECT ADVANCED LEVEL" src="https://user-images.githubusercontent.com/122585172/230769103-3941b640-d92b-4c83-ad0a-9016407bfb1f.png">


Prerequisites:
1. Nexus 
2. Sonarqube
3. Maven Installed
4. Docker & Dockerhub account
5. AWS
6. Jenkins 

Here we will see some Key points:

1. Application Overview
2. Git use cases
3. Jenkins Job Creation 
4. Maven UNIT TEST
5. Maven Integration TEST
6. Maven Building jar/War files
7. SonarQube Configuration
8. Sonarqube-webhook Configuration 
9. Static code Analysis 
10. QualityGate Status  
11. Nexus Repo Overview
12. Release Repo creation 
13. Snapshot repo creation  & Configuration
15. Multistage DockerFile 
16. Docker Image Build
17. Docker Image Push



Step: 1 Installation Part

Push all the web application page code file into github

![trytry](https://user-images.githubusercontent.com/122585172/230770031-f6f7d157-2010-4155-91ab-91e2ddbdbe13.png)

1. For Jenkins  install you need to follow here: https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

After install you will look like this:

![12 04 2023_18 28 54_REC](https://user-images.githubusercontent.com/122585172/231465002-4278d3ba-0fbd-4bd6-91bd-426d9c48984d.png)

2. For Sonarqube install:  you need to install docker before executing this command docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

After install sonarqube  will look like this:

![12 04 2023_18 30 54_REC](https://user-images.githubusercontent.com/122585172/231465551-2e7c6667-758b-4349-9705-c228ef521fbb.png)

3. For nexus: 
you need to follow step by step:

apt-get update -y

echo "Install Java"
apt-get install openjdk-8-jdk -y
java -version

echo "Install Nexus"
useradd -M -d /opt/nexus -s /bin/bash -r nexus
echo "nexus ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/nexus
mkdir /opt/nexus
wget https://sonatype-download.global.ssl.fastly.net/repository/downloads-prod-group/3/nexus-3.29.2-02-unix.tar.gz
tar xzf nexus-3.29.2-02-unix.tar.gz -C /opt/nexus --strip-components=1
chown -R nexus:nexus /opt/nexus

nano /opt/nexus/bin/nexus.vmoptions

https://www.howtoforge.com/how-to-install-and-configure-nexus-repository-manager-on-ubuntu-20-04/

After install Nexus look like this:


![12 04 2023_18 32 48_REC](https://user-images.githubusercontent.com/122585172/231466061-5445e124-094a-416b-8caa-f363b264eceb.png)

4. Docker install and create dockerhub account

For docker you need to do follow  step by step:https://docs.docker.com/engine/install/ubuntu/

Create dockerhub account

![fgfgf](https://user-images.githubusercontent.com/122585172/230771181-dde8e9ba-1fd6-4340-ab0b-dc60d9455be0.png)


***Done with Installation , Now will we integrate all the tools with Jenkins***

Step-01 : Sonarqube  integration with Jenkins

First thing you need to do you will install sonarqube plugin like sonarqube Generic plugin , sonar gerit plugin , Quality gate plugin, sonar quality gate plugin

![12 04 2023_18 36 18_REC](https://user-images.githubusercontent.com/122585172/231466905-e0687559-e098-445a-bbde-d81cbb2d36a3.png)



Step-02 : Nexus  integration with Jenkins
you need plugin for integration nexus with jenkins like we have Nexus Artifact Uploader

![tryrtyt](https://user-images.githubusercontent.com/122585172/230771942-08bf229b-94ed-427e-ab37-23b8b2ab894d.png)

you need to install one  remain plugin like we have pipeline utilit steps


We integrated all the tools with Jenkins, Now Create a declarative jenkins pipeline for each stage.


Stage 01: Git checkout

Under this step there will be steps

1. If you don't konw how to write syntax for that you will just go back and click on pipeline syantax / click on git / provide the repo url /then click genrate pipeline script


![dfghdfh](https://user-images.githubusercontent.com/122585172/230772671-195522aa-0243-4692-8263-66f6d6303bc2.png)

Stage 02: UNIT TESTING

1. we just have simple command for that it's a type of shell script  sh 'mev test' make sure you installed the maven 


![fdgdfg](https://user-images.githubusercontent.com/122585172/230772928-323f407e-3eb8-44d2-9c88-8f19f1386e3f.png)

Stage 03: Integration test

01. under stpes you have types commands whatever you  going to use  command sh 'mvn -DskipUnitTests'

![fdgfdg](https://user-images.githubusercontent.com/122585172/230773142-b8efac60-de9f-4270-8081-655d4b35c638.png)

Stage 04: Maven build

01. under that we have steps and we have a command sh sh 'mvn clean install' it will do what ? 
02. it will clean all the war files whatever is before installed and all and it will try to install from the new end so that is why it's cleaning and  it's going to install files again and again whatever packges and libarey we need require run the this java application. 


![fgddg](https://user-images.githubusercontent.com/122585172/230773520-bd56e181-eaec-4d0f-a3b6-bc4fd4222455.png)

 
 Stage 05: Static code analysis
 
01. so here we have to write the command for Static code analysis so for that what we have to do make a connection from the jenkins to your sonarqube make sure you make connection between them 

02 so that is why it will do it will do authenticate and it will try to clean package those artifact and it will try to send those all artifact to the sonarqube server.

![fdssdg](https://user-images.githubusercontent.com/122585172/230773902-b8b41709-8571-4364-8e98-8ae30321f085.png)


Stage 06: Quality Gate Status

01. for that you can go directly jenkins click on pipeline syntax/select waitforqualitygate/provide your authentication/genrate pipeline syntax.

![gdfdfd](https://user-images.githubusercontent.com/122585172/230774447-6983ba9d-b284-4c12-8982-8005a02af2bc.png)

Stage 07: Nexus Artifact uploader

![hgjghj](https://user-images.githubusercontent.com/122585172/230774637-1f62be6d-304b-4e42-b86b-c7f4b93ba466.png)

Create a Multisatge Dockerfile

![fdgfdgfd](https://user-images.githubusercontent.com/122585172/230774751-b6fd4409-82a8-466f-86ab-0b61040c6203.png)

Stage 08: Docker image building

01. Make sure docker is installed on your jenkins server then you able run this command and here  what i can do i will jsut make a this version the taging version dynamically 


 02. whenever jenkins build number run when ever i will build the pipeline based on that the tags should get updated for that what have to do we have taging that way. 

03. i can use $job_name or version and build id it will build image this way .

04. once you  build that image you can tag those image as well so you can easily pushed to dockerhub.

![fghfghg](https://user-images.githubusercontent.com/122585172/230775338-36120421-48db-489d-91ab-48c645c58ba4.png)

Stage 09: Push image to Dockerhub

01. before pushing the image dockerhub what you have to do you have to do just login your dockerhub account .

02. Go to pipeline syntax/ select withCredentials.

![hgjhgj](https://user-images.githubusercontent.com/122585172/230775594-e4cdd6de-f981-4138-b9a5-52d555acb9e2.png)


Final outputs of this Project


Jenkins Output :

![retret](https://user-images.githubusercontent.com/122585172/230775796-af383333-80ca-4bda-8f89-2b219ffbc90d.png)

Sonarqube Output:

![dfgfdfd](https://user-images.githubusercontent.com/122585172/230775913-ffedf365-29a7-4204-adb2-af7aaaa20500.png)

Quality Gate Status in Jenkins:

![fgfhgfh](https://user-images.githubusercontent.com/122585172/230775982-f6535b91-dedc-444f-bd50-7f03a6563927.png)

Images in DockerHub pushed by jenkins:

![sdfdsfd](https://user-images.githubusercontent.com/122585172/230776072-c1b5cfb5-d09b-412e-b785-c401acb8c085.png)

Nexus stored Artifact/snapshot output:

![retretr](https://user-images.githubusercontent.com/122585172/230776162-c1e480ef-7143-4bd0-9868-3b055583f7b5.png)








