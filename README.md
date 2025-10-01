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

```http Eclipse Temurin Installer
```
```http SonarQube Scanner  
```

