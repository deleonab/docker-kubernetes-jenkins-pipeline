### Setting up a Kubernetes and Jenkins pipeline in AWS
### We shall first set up the Jenkins server on a virtual machine (EC2)
SPIN EC2 INSTANCE FOR OUR JENKINS SERVER

- Launch EC2 Ubuntu T2 Medium
- Save pem key for SSH Tasks
- Open port 8080 for jenkins in security group and 22 if not already open
- CHMOD the pem key to 660
```
chmod 660
```
![Ec2 created](./images/ec2-created.JPG)


