# Java-twitter-App
**Create a Ubuntu server in aws for Jenkins, Sonarqube and Nexus** 
instance = t2.targe
memory  = 40GB

**1\.Update all system**

apt-get update


**2\. Install java 17**

sudo apt install openjdk-17-jdk

**3\. Install Jekins**

```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]  https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
sudo systemctl start jenkins
```

instll trivy wherever jenkins is running --- if required 

sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -

echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list

sudo apt-get update

sudo apt-get install trivy


# In JENKINS - type docker it will give command to install docker
sudo chmod 666 /var/run/docker.sock
# Login to jenkins after installing pluggins

# IN Nexus - install docker
# Create nexus using docker
sudo docker run -d -p 8082:8082 sonatype/nexus3

Sign in to nexus 

username = admin

get password login in to nuxus docker

sudo docker exec -it cont-id /bin/bash

cd sonartype-work

cd nexus3

cat admin.password

do not copy bash 

enable aonyms acces

# In SOnaqube - install docker
# Create sonarqube using docker  - free community version
sudo docker run -d -p 9000:9000 sonarqube:lts-community

login 

username = admin

password = admin

Generate token in sonarqube

COnfigure sonarqube server in jenkins

# IN JENKINS instll pluggins
1. sonarqube-scanner
2. Config file  provider
3. maven integeration
4. pipeline maven integration
5. kubernet
6. kubernetes client api
7. kubernetes cred
8. kubernetes cli
9. docker
10. docke pipeline
11. eclipse temurin installer
12. pipeline.stage view
    
# Configure tools in JENKINS
1. Docker
   Name
   install auto
   downloan from docker.com
   latest
2. maven - lates
3. Sonarqube
   sonar_scanner
4. Add JDK if you want to use different version
   jdk17
   install from adoptium
   select ver 17
# Create project with pipeline and write pipeline
# While writing pipeline whichever tools we are going to use we have define in pipeline
# Name in pipeline here should give same as when created in tools

 pipeline{
 
   agent any
   
   tools{
   
   jdk 'jdk17'
   
   maven 'maven3'
   }
# Add groovy script in pipeline
# CRedentions can be created in credentioal section for git (if private), docker, sonarqube, neuxs etc
# Add sonarqube credentials and add server in system (jenkins)
name

Sonarqube URL

Select sonarqube Token(cred)

# IN order to publish our artifacts to nexus
1. Jenkins should be able to comm with nuxus
   
3. Cred and URL of nexus should be available to jenkins
   
5. Add URL in pom.xml
   
7. go to nexus -->  browse --> copy maven releases and maven snapshots ---> paste in URL added in pom.xml
   
