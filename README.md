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

![gdfdfg](https://user-images.githubusercontent.com/122585172/230770151-5f53be7e-5351-437b-be93-85e80772bf22.png)

2. For Sonarqube install:  you need to install docker before executing this command docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

After install sonarqube  will look like this:

![tyrtyu](https://user-images.githubusercontent.com/122585172/230770832-72002f65-864c-4af3-a294-0c7072dee396.png)

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

![ytutyuyu](https://user-images.githubusercontent.com/122585172/230770905-77856f57-0f3b-4d37-bff3-a0293618be34.png)

4. Docker install and create dockerhub account

For docker you need to do follow  step by step:https://docs.docker.com/engine/install/ubuntu/

Create dockerhub account

![fgfgf](https://user-images.githubusercontent.com/122585172/230771181-dde8e9ba-1fd6-4340-ab0b-dc60d9455be0.png)


***Done with Installation , Now will we integrate all the tools with Jenkins***

Step-01 : Sonarqube  integration with Jenkins

First thing you need to do you will install sonarqube plugin like sonarqube Generic plugin , sonar gerit plugin , Quality gate plugin, sonar quality gate plugin

![dfsdsf](https://user-images.githubusercontent.com/122585172/230771699-1c1957db-6392-4968-aaa6-92d6efd9d413.png)

Step-02 : Nexus  integration with Jenkins
you need plugin for integration nexus with jenkins like we have Nexus Artifact Uploader

![tryrtyt](https://user-images.githubusercontent.com/122585172/230771942-08bf229b-94ed-427e-ab37-23b8b2ab894d.png)

you need to install one  remain plugin like we have pipeline utilit steps


We integrated all the tools with Jenkins, Now Create a declarative jenkins pipeline for each stage.


Stage 01: Git checkout

Under this step there will be steps

1. If you don't konw how to write syntax for that you will just go back and click on pipeline syantax / click on git / provide the repo url /then click genrate pipeline script







