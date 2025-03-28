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

**4\. Install trivy wherever jenkins is running**

sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -

echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list

sudo apt-get update

sudo apt-get install trivy


**5\. Install the docker**
```
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt-cache policy docker-ce
```

**6\. Login to jenkin --> Goto Pluggins --> Install pluggins**

1.sonarqube-scanner

2.Config file provider

3.maven integeration

4.pipeline maven integration maven

5.nexus artifact uploader

6.docker

7.owasp

8.docke pipeline

9.eclipse temurin installer

10.pipeline.stage view


**7\. Create Nexus conatiner using docker image**

sudo docker run -d -p 8082:8082 sonatype/nexus3

Sign in to nexus 

username = admin

get password by login in to nuxus docker

sudo docker exec -it cont-id /bin/bash

cd sonartype-work

cd nexus3

cat admin.password

Capy password (do not copy bash) 

**8\. Create sonarqube using docker  - free community version**

sudo docker run -d -p 9000:9000 sonarqube:lts-community

login 

username = admin

password = admin

Generate token in sonarqube

COnfigure sonarqube server in jenkins
    
**9\. Configure tools in JENKINS**

1. JDK
2. Docker
3. maven
4. Sonarqube
5. OWASP

**10\. Create project with pipeline and write pipeline**

**Notes**

1. While writing pipeline whichever tools we are going to use we have define in pipeline
2. Tools name in pipeline should be give same as when defining in tools

**Add groovy script in pipeline**
**Add credentions for git (if private), docker, sonarqube in credentials section in Jenkins**
**Add sonarqube server jenkins system**

# IN order to publish our artifacts to nexus
1. Jenkins should be able to comm with nuxus
   
3. Cred and URL of nexus should be available to jenkins
   
5. Add URL in pom.xml
   
7. go to nexus -->  browse --> copy maven releases and maven snapshots ---> paste in URL added in pom.xml
   
