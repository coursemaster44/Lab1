
# Lab1

EC2 Lab With Manual Apache
------------------------------

**Step 1.Goto AWS Management Console>AWS Services>Find services>Type EC2>Click on EC2>EC2 Dashboard>Instances>Launch Instances**

**Step 2.Choose AMI(Amazon Machine Image) Amazon linux 2 AMI Free tier eligible,Click to Select**

**Step 3.Choose Instance type**
 - Type t2.micro Free tier 
 - vCPUs-1 
 - Memory-1Gib

Click on Next-Configure Instance details

**Step 4.Configure Instance details**
- Number of Instances- type 1
- Network-Default VPC
- Subnet- No preference
- Auto assign Public IP-Use Subnet setting (Enable)
- IAM Role
- User Data

  Click on Next:Add Storage

**Step 5. Next Add Storage**
- Keep Default Size-8 Gib

  Click Next:Add Tags

**Step 6. ADD Tags**
  Leave as of now
  
  Click on Next:Configure Security Group

**Step 7.Configure Security Group**
 -SSH already there
 -Add Rule for HTTP

Click Review and Launch >Launch

**Step 8. Review**
Select an existing key pair or create a new key pair

- Select create a new pair
- Provide key pair name
- Click on Download key pair 
- Launch instance

**Step 9. Click on the launched Instance and Click on Details to see the Public IP and other details.**

**Step 10. Ec2 dashboard>Instances>Launched Instance>Actions>Connect**

**Step 11. Run the Following Commands**

```sh
$ sudo su
$ yum update -y
$ yum install -y httpd
$ systemctl start httpd.service
$ systemctl enable httpd.service
$ echo "Hello World from $(hostname -f)" > /var/www/html/index.html
$ cd /var/www/html
$ ls -a
$ echo "Hello World from $(hostname -f)" > /var/www/html/index.html
$ ls -a
$ cat index.html
```

**Step 12. Copy the Public IP and paste in the browser to see Apache Web server is Running**

### End Of Lab






# Lab2

Ec2 Lab With User Data Apache
------------------------------

**Step 1. Goto AWS Management Console>AWS Services>Find services>Type EC2>Click on EC2>EC2 Dashboard>Instances>Launch Instances**

**Step 2.Choose AMI(Amazon Machine Image) Amazon linux 2 AMI Free tier eligible,Click to Select**

**Step 3.Choose Instance type**
 - Type t2.micro Free tier 
 - vCPUs-1 
 - Memory-1Gib

Click on Next-Configure Instance details

**Step 4.Configure Instance details**
- Number of Instances- type 1
- Network-Default VPC
- Subnet- No preference
- Auto assign Public IP-Use Subnet setting (Enable)
- IAM Role
- Advance Details>User Data
    - Select As Text

```sh
#bin/bash
yum update -y
yum install -y httpd
systemctl start httpd.service
systemctl enable httpd.service
echo "Hello World from $(hostname -f)" > /var/html/index.html
```

  Click on Next:Add Storage

**Step 5.Next Add Storage**
- Keep Default Size-8 Gib

  Click Next:Add Tags

**Step 6. ADD Tags**
  Leave as of now
  
  Click on Next:Configure Security Group

**Step 7.Configure Security Group**
 -SSH already there
 -Add Rule for HTTP

Click Review and Launch>Launch

**Step 8. Review**
Select an existing key pair or create a new key pair

- Select create a new pair
- Provide key pair name
- Click on Download key pair 
- Launch instance

**Step 9. Click on the launched Instance and Click on Details to see the Public IP and other details.**

**Step 10. Ec2 dashboard>Instances>Launched Instance>Actions>Connect**

**Step 11. Copy the Public IP and paste in the browser to see Apache Web server is Running**

### End Of Lab

# Lab3

### lab3-ElasticBeanStalk

**Step 1. Goto AWS Management Console>AWS Services>Find services>Type Elastic Beanstalk>Click on Elastic Beanstalk>Elastic Beanstalk>Create Application**


**Step 2. Create a Web App**
   - Application Name-MyfirstEbsapp
		 
		 - Platform 
		    - Platform 
		       - Node.js
			- Platform branch
			   - Node.js 12 running on 64bit Amazon Llinux2
			- Platform version
			   - 5.2.3(Recommended)
			   
	  
   - Application Code
			   - Select Sample application
			 
	
 Click on Create Application.
	


**Step 3. Creating environment started**

Elastic BeanStalk launches an environment named MyfirstEbsapp-env with these AWS resources:

 - S3 Bucket

 - Target Group

 - Security Group for ec2 instance
 
 - Security Group for ALB
 
 - Auto Scaling launch configuration
 
 - Auto Scaling Group
 
 - Auto Scaling Policies
 
 - CloudWatch Alarms
 
 - Load Balancer
 
 - Load balancer listener

 - EC2 instance


**Step 4. Check the environment**

- The environment overview pane shows its URL,current health status, the application version,platform version  

- Click on MyfirstEbsapp>Application versions

- Click on MyfirstEbsapp-env

Click on Go to environment



**Step 5. Goto each component and verify the resources created by Elastic BeanStalk**


   - S3 Bucket
        -Goto AWS Console>All Services>S3>Buckets
        
   
   - Auto Scaling launch configuration
         - AWS Console>Services>Ec2>Auto Scaling>launch configuration>User Data>View User Data
         
		
   - Auto Scaling Group
         - AWS Console>Services>Ec2>Auto Scaling>Auto Scaling Groups
         
		 
   - EC2 instance
         - AWS Console>All services>EC2 >Instances>    
         
		
   - Target Group
         - Goto AWS Console>All Services>EC2>Load Balancer>Target Group>Targets
		 
   
   - Load Balancer
         - AWS Console>Services>EC2>Load Balancing>Load balancers>awseb-AWSEB-LoadBalancer>Listeners>Edit
         
	
  -  Security Groups
         - Goto AWS Console>All Services>EC2>Security Groups
         
		 
  -  CloudWatch Alarms
         - AWS Console>Services>CloudWatch>Alarms>Alarm	 
		 
		 

**Step 6.ElasticBeanStalk>Applications>MyfirstEbsapp>Application versions**

  Click on Sample Application>nodejs.zip
  
  Download the nodejs.zip
  
  
  
  # End of Lab
  
