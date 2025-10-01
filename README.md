# Netflix-project-using-Jenkins
# Deploy Netflix Clone on Cloud using Jenkins - DevSecOps Project!
![image alt](https://github.com/Prathameshkokane4565/Netflix-project-using-Jenkins/blob/4b066150b68d08191dafbfde857e283fd80c661c/home-page.png)
                                   home page

# Launch EC2 (Ubuntu 22.04):  
  1. Provision an EC2 instance on AWS with Ubuntu 22.04.
  2. Connect to the instance using SSH.

# Phase 3: CI/CD Setup
 1.Install Jenkins for Automation:
  #### Install Jenkins on the EC2 instance to automate deployment: Install Java
 ```http
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

#### > Access Jenkins in a web browser using the public IP of your EC2 instance.

publicIp:8080

# 2.Install Necessary Plugins in Jenkins:

Goto Manage Jenkins →Plugins → Available Plugins → Install below plugins

```http
 Eclipse Temurin Installer
```
```http
SonarQube Scanner  
```
```http
NodeJs Plugin
```
```http
docker
```
```http
stage view
```
## Configure Java and Nodejs in Global Tool Configuration
#### Goto Manage Jenkins → Tools → Install JDK(17) and NodeJs(16)→ Click on Apply and Save

#### JDK
![image alt](https://github.com/Prathameshkokane4565/Netflix-project-using-Jenkins/blob/b0876bfb3080ea65e256be008b1f0be92e121776/Screenshot%202025-10-01%20210426.png)

#### Sonarqube Scanner
![image alt](https://github.com/Prathameshkokane4565/Netflix-project-using-Jenkins/blob/265cb9f15bd0dd406068b83e67f608adecd6ee52/sonar.png)

#### Docker
![image alt](https://github.com/Prathameshkokane4565/Netflix-project-using-Jenkins/blob/ff21a1af425f6253dacf320e237b1a3784af9c0e/docker.png)

#### Node.js
![image alt](https://github.com/Prathameshkokane4565/Netflix-project-using-Jenkins/blob/13aa738091d8b947017f4b38a47aa89f546b04b5/Node%20JS.png)

#### Install Docker and Run the App Using a Container:

 >Set up Docker on the EC2 instance:
```http
sudo apt-get update
sudo apt-get install docker.io -y
sudo systemctl start docker
sudo usermod -aG docker ubuntu
sudo usermod -aG docker jenkins
newgrp docker
sudo chmod 777 /var/run/docker.sock
```
## Phase 2: Security

1.Install SonarQube and Trivy:

>Install SonarQube and Trivy on the EC2 instance to scan for vulnerabilities.
sonarqube
```http
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```
To access:

publicIP:9000 (by default username & password is admin)
![image alt](







#### Global Tool Configuration is used to configure different tools that we install using Plugins

We will install a sonar scanner in the tools.

Create a Jenkins webhook

Configure CI/CD Pipeline in Jenkins:
Create a CI/CD pipeline in Jenkins to automate your application deployment.
