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

- Install SonarQube and Trivy on the EC2 instance to scan for vulnerabilities.
sonarqube
```http
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```
To access:

publicIP:9000 (by default username & password is admin)
![image alt](https://github.com/Prathameshkokane4565/Netflix-project-using-Jenkins/blob/62d8873204c004ecee8d7ec7f867d88f14675b01/sonar%20qube%20login.png)

#### To install Trivy:
```http
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```      
#### To scan image using trivy

```http
trivy image <imageid>
```
2.Integrate SonarQube and Configure:
- Integrate SonarQube with your CI/CD pipeline.
- Configure SonarQube to analyze code for quality and security issues.
####SonarQube
Create the token
Go to Jenkins Dashboard → Manage Jenkins → Credentials → Add Secret Text. It should look like this
![image alt](https://github.com/Prathameshkokane4565/Netflix-project-using-Jenkins/blob/6e1e33826662cb28c954a488da5e2072e3a316f0/sonar%20scrate%20key.png)

After adding sonar token

Click on Apply and Save

#### The Configure System option is used in Jenkins to configure different server
![image alt](https://github.com/Prathameshkokane4565/Netflix-project-using-Jenkins/blob/fcf7845630e38b7cc235209f6cf1e77fe4a64d90/sonar%20server.png)

#### Global Tool Configuration is used to configure different tools that we install using Plugins

We will install a sonar scanner in the tools.

Create a Jenkins webhook

Configure CI/CD Pipeline in Jenkins:
Create a CI/CD pipeline in Jenkins to automate your application deployment.

```http
pipeline {
    agent any
    tools {
        maven 'maven'
    }
    
    stages{
        stage('code-pull'){
            steps {
                git branch: 'main', url: 'https://github.com/Prathameshkokane4565/Project-InsureMe.git'
            }
        }
        
        stage('code-build'){
            steps{
                sh "mvn clean package"
            }
        }

        stage('code-deploy'){
            steps{
                sh "docker build -t insureme ."
                sh "docker run -itd --name mycont -p 8089:8081 insureme"
            }
        }

    }
}
```







Configure CI/CD Pipeline in Jenkins:
Create a CI/CD pipeline in Jenkins to automate your application deployment.


## Cleanup AWS EC2 Instances: - Terminate AWS EC2 instances that are no longer needed.
