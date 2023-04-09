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

For Jenkins  install you need to follow here: https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

After install you will look like this:

![gdfdfg](https://user-images.githubusercontent.com/122585172/230770151-5f53be7e-5351-437b-be93-85e80772bf22.png)

For Sonarqube install:  you need to install docker before executing this command docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

After install sonarqube  will look like this:

![tyrtyu](https://user-images.githubusercontent.com/122585172/230770832-72002f65-864c-4af3-a294-0c7072dee396.png)

For nexus: 
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



