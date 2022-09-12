### Setting up a Kubernetes and Jenkins pipeline in AWS
### We shall first set up the Jenkins server on a virtual machine (EC2)
SPIN EC2 INSTANCE FOR OUR JENKINS SERVER

- Launch EC2 Ubuntu T2 Medium
- Save pem key for SSH Tasks
- Open port 8080 for jenkins in security group and 22 if not already open
- CHMOD the pem key to 660
```
chmod +660 mynewkeypair.pem
```
![Ec2 created](./images/ec2-created.JPG)


### I WILL NOW CONNECT TO MY EC2 INSTANCE VIA SSH
- Go to my instance > SSH client and copy connection string

```
ssh -i "mynewkeypair.pem" ubuntu@ec2-3-8-206-166.eu-west-2.compute.amazonaws.com
```

### UPDATE, install JDK, THEN JENKINS

```
sudo apt-get update
```
### Check if Java installed

```
java -version
```
### Not installed so I will install java
```
sudo apt install openjdk-11-jre-headless
```

1. Add Jenkins repository to package managaer
```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -

sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list' 
```
### Update the package manager
```
sudo apt-get update
```
### Install Jenkins
```
sudo apt install jenkins
```
### Check that |jenkins is installed and running 
```
sudo systemctl status jenkins
```
## I WILL NOW LOG INTO JENKINS VIA BROWSER USING THE ec2 instances public IP address on port 8080
```
3.8.206.166:8080
```
### got to /var/lib/jenkins/secrets/initialAdminPassword for Password

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
### copy and enter password on 3.8.206.166:8080

- select Install suggested plugins option

### WE NEED TO GIVE ADMIN PRIVILEGES TO JENKINS TO BE ABLE TO RUN OUR PIPELINE (DOCKER,GRADLE, KUBERNETES )
To interact with the Kubernetes cluster, Jenkins will be executing the shell script with the Jenkins user, so the Jenkins user should have thenecessary privileges.

I will add Jenkins as an administrator and assign NOPASSWD so that the root password wouldn't be requested when the pipeline is running.

Open the file /etc/sudoers

```
sudo vi /etc/sudoers
```
Assign admin priviledge and no password required
```
jenkins ALL=(ALL) NOPASSWD: ALL
```
### and then :wq! to save and quit vi
### Now i have given jenkins the privileges it needs
```
sudo su - jenkins
```
![jenkins user](./images/jenkins-user.JPG)
