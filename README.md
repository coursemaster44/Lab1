
# Lab1

EC2 Lab With Manual Apache
------------------------------

**Step 1. Goto AWS Management Console>AWS Services>Find services>Type EC2>Click on EC2>EC2 Dashboard>Instances>Launch Instances**

**Step 2. Choose AMI(Amazon Machine Image) Amazon linux 2 AMI Free tier eligible,Click to Select**

**Step 3. Choose Instance type**
 - Type t2.micro Free tier 
 - vCPUs-1 
 - Memory-1Gib

Click on Next-Configure Instance details

**Step 4. Configure Instance details**
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

**Step 7. Configure Security Group with following settings**
 - Type SSH is already with port 22 open from anywhere 0.0.0.0/0
 - Add rule for Type HTTP with port 80 open from anywhere 0.0.0.0/0

Click Review and Launch 

**Step 8. Review Instance Launch**

Click on Launch
- Now Select an existing key pair or create a new key pair
  - Select create a new pair
  - Provide key pair name
  - Click on Download key pair 
  
  Click on Launch instances

**Step 9. Click on the launched Instance-id and Click on Details to see the Public IP and other details.**

**Step 10. Ec2 dashboard>Instances>Launched Instance>Actions>Connect>Ec2 Instance Connect>Connect**

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
$ cat index.html
```

**Step 12. Copy the Public IP and paste in the browser to see Apache Web server is Running**

### End Of Lab






# Lab2

Ec2 Lab With User Data Apache
------------------------------

**Step 1. Goto AWS Management Console>AWS Services>Find services>Type EC2>Click on EC2>EC2 Dashboard>Instances>Launch Instances**

**Step 2. Choose AMI(Amazon Machine Image) Amazon linux 2 AMI Free tier eligible,Click to Select**

**Step 3. Choose Instance type**
 - Type t2.micro Free tier 
 - vCPUs-1 
 - Memory-1Gib

Click on Next-Configure Instance details

**Step 4. Configure Instance details**
- Number of Instances- type 1
- Network-Default VPC
- Subnet- No preference
- Auto assign Public IP-Use Subnet setting (Enable)
- IAM Role
- Advance Details>User Data
    - Select As Text

```sh
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd.service
systemctl enable httpd.service
echo "Hello World from $(hostname -f)" > /var/www/html/index.html
```

  Click on Next:Add Storage

**Step 5. Next Add Storage**
- Keep Default Size-8 Gib

  Click Next:Add Tags

**Step 6. ADD Tags**
  Leave as of now
  
  Click on Next:Configure Security Group

**Step 7. Configure Security Group**
 -SSH already there
 -Add Rule for HTTP

Click Review and Launch

**Step 8. Review Instance launch**
Click on Launch
- Select an existing key pair or create a new key pair
  - Select create a new pair
  - Provide key pair name
  - Click on Download key pair 

Click on Launch instances

**Step 9. Click on the launched Instance and Click on Details to see the Public IP and other details.**

**Step 10. Ec2 dashboard>Instances>Launched Instance>Actions>Connect**

**Step 11. Copy the Public IP and paste in the browser to see Apache Web server is Running**

### End Of Lab





# Lab3

### lab3-ElasticBeanStalk
-----------------------------------------------------------------------------------------------------------------------------------------------------------

**Step 1. Goto AWS Management Console>AWS Services>Find services>Type Elastic Beanstalk>Click on Elastic Beanstalk>Elastic Beanstalk>Create Application**


**Step 2. In Create a Web App**
   - Application Name - MyfirstEbsapp
		 
   - Platform 
     - Platform 
       - Node.js 
     - Platform branch
       - Node.js 12 running on 64bit Amazon Llinux2
     - Platform version
       - 5.2.3(Recommended)
			   
   - Application Code- Select Sample application
			 
	
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

Click on Go to environment to see sample application running



**Step 5. Goto each component and verify the resources created by Elastic BeanStalk**


   - S3 Bucket
     -Goto AWS Console>All Services>S3>Buckets>elasticbeanstalk-ap-south-1-XXXX
        
   
   - Auto Scaling launch configuration
         - AWS Console>Services>Ec2>Auto Scaling>launch configuration>User Data>View User Data
         
		
   - Auto Scaling Group
         - AWS Console>Services>Ec2>Auto Scaling>Auto Scaling Groups>awseb-a-xxx
         
		 
   - EC2 instance
         - AWS Console>All services>EC2 >Instances>Myfirstebsapp-env   
         
		
   - Target Group
     - Goto AWS Console>All Services>EC2>Load Balancer>Target Group>awseb-AWSEB-xxxx
		 
   
   - Load Balancer
     - AWS Console>Services>EC2>Load Balancing>Load balancers>awseb-AWSEB-LoadBalancer>Listeners>Edit>See Forward to-xx
         
	
  -  Security Groups
     - Goto AWS Console>All Services>EC2>Security Groups
       - 2 SGs with name Myfirstebsapp-env
         
		 
  -  CloudWatch Alarms
         - AWS Console>Services>CloudWatch>Alarms
	   - 2 alarms(Scale-in,scale-out) created awseb-xxx 
		 


**Step 6. ElasticBeanStalk>Applications>MyfirstEbsapp>Application versions**

  - Click on Sample Application>nodejs.zip
  
  - Download the nodejs.zip
  
  
  
  # End of Lab
  

lab4#ElasticBeanstalk-2
--------------------------------------------------------------------------------------------------------------------------------------------------

**Step 1. Open Downloaded node.js Application from AWS  in Visual Studio Code and modify it for background color**
- Link to Download - https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/nodejs-getstarted.html

**Step 2. Save the modification in this file as nodejs2.zip**

**Step 3. Elastic BeanStalk>Applications>MyfirstEbsapp>Application versions>upload>Sample application-1>choose file>nodejs(2).zip>upload**

**Step 4. Select Sample application-1>Actions>Deploy>Deploy**
- Error: Failed to deploy because of some Zipped files 

**Step 5. Now Open VS Code>index.html>Terminal**
- To Remove _MACOSX run the following command

```sh
zip -r dir.zip . -x "_MACOSX"
```

**Step 6. MyfirstEbsapp>Application versions>upload>Sample application-2>choose file>dir.zip>upload**

**Step 7. Select Sample application-2>Actions>Deploy>Deploy**

**Step 8. ElasticBeanStalk>Environments>Myfirstebsapp-env>Events**

**Step 9. ElasticBeanStalk>Environments>Myfirstebsapp-env**

 - Click on Application URL 
 - Backround color has been changed
 
 **Step 10. ElasticBeanStalk>Environments>Myfirstebsapp-env>Upload and Deploy** 
 - Click if you want to modify again
 
 **Step 11. Elastic BeanStalk>Applications>MyfirstEbsapp>Actions>Create Environment>Web server environment**
 - Select Web server environment to create new environment from this application
 
# End of Lab

# lab5.1#Git-Installation-MACOS-lab
------------------------------------------------------------

**Open Terminal in MACOS**
- Run the following commands to install Git

``` sh
$ git --version
$ brew update && brew upgarde
$ brew install git
$ brew link --force git
$ git --version
```
# End of Lab

# lab 5.2 Download & install Git on Windows
---

**Step 1. Open internet Browser and Search for Download git for windows. 
Click on "Downloads git" link**

**Step 2. Click on Download 2.28.0 for windows**

**Step 3  Click on the downloaded file GIT-2.28.0-64-bit.exe**

**Step 4. Click on Run**

**Step 5. Click Next**

**Step 6. Select Destination Location and Click on Next**

**Step 7. Select Components and  Click on Next**

**Step 8. To continue,click Next.If you would like to select a different folder,click Browse.**

**Step 9. Select Use Git from the Windows Command Prompt**
- Click on Next

**Step 10. Select Use the OpenSSL library and Click on Next**

**Step 11. Select Checkout Windows-style,commit unix style and Click on Next**

**Step 12. Select Use MinTTY and Click Next**

**Step 13. Select Enable file system caching and Enable Git credentials Manager and Click Next**

**Step 14. Click Install**

**Step 15. Installation has been started**

**Step 16. Select Launch Git bash**
- Click on Finish

**Step 17. Open Local PC and Goto Start>Git Bash**

```
Type #“git init” to initialize the git
Type  #“mkdir” to make a new directory(folder)
Type # “cd test” to move into test directory

```

# End of lab




# lab6#ALB Lab-1
-----------------------------
**Step 1. Go to AWS Console>All Services>EC2>Load Balancing>Target Groups>Create Target Group**

**Step 2. Specify group details as following**
-   Select Instances in target type  
-   Target group name as MyFirstTargetgroup
-   Protocol-HTTP,Port-80
-    VPC-Default
-    Protocol version
-    Health Checks
	  - Health check protocol- HTTP
	   - Health check path- /
		  
**Now Click on Next**

**Step 3. Register targets**
          
- Select the available instances
- Ports for the selected instances-80
- Click on "Include as pending below"
		   
**Now Click on Create target group**
		   
**Step 4. "MyFirstTargetgroup" Target Group has been created**

**Step 5. Goto MyFirstTargetgroup>Targets>Registered targets**
              
 - Status is showing "unused"
			  
**Step 6. Go to AWS Console>All Services>EC2>Load Balancing>Load Balancers>Create load balancer**

**Step 7. Click on Create in Application Load Balancer**

**Step 8. Configure Load Balancer as following**
		 
- Basic Configuration
	- Name- MyFirstALB
	- Scheme- internet-facing
	- Ip address type- ipv4
-  Listeners-Protocol-HTTP,Port-80
-  Availability Zones
   - VPC-Default
   - Availability Zones-Select all Zones 
   
Click on Next:Configure Security Settings

**Step 9. Click on Next:Configure Security Groups** 
  -  Create a new security group
	- Type-Custom TCP
        - Protocol-TCP
        - Port Range-80	
        - Source-Custom(0.0.0.0./0)	

Click on Next:Configure Routing

**Step 10. Configure Routing**
          
- Target group- Select Existing target group Name-MyFirstTargetgroup
		  
Click on Register Targets

**Step 11. Click on Next:Review**

**Step 12. Click on Create**
Click on Close

**Step 13. Goto AWS Console>All Services>EC2>Load Balancing>Load Balancers>MyFirstALB**
- It will take some time for state change from provisioning to active

**Step 14. Copy the DNS name from the description of ALB**

**Step 15. Paste the DNS name in Internet Browser**
           
- Hit refresh 3 times to see the Traffic is going on all the 3 instances

**Step 16. Go to AWS Console>All Services>EC2>Load Balancing>Load Balancers>MyFirstALB>Listeners**

- Select listener and Click on Edit
		   
**Step 17. Go to AWS Console>All Services>EC2>Load Balancing>Load Balancers>Target groups>MyFirstTargetgroup>Targets**	  


Lab7# ASG-Lab
---------------------------------
**Step 1. Goto AWS Console>EC2 Dashboard>Instances>Lunch Templates>Create launch template**

**Step 2. In Create Lunch template give as following-**
- Launch template name-MyFirstTemplate

- Amazon Machine image(AMI)-Amazon Linux 2

- Instance type-t2.micro

- key pair-select your key pair

- Virtual Private Cloud

- Select the Security groups

- Storage

- Advanced details:-
 - User data
``` sh
#!bin/bash
yum update -y
yum install -y httpd
systemctl start httpd.service
systemctl enable httpd.service
echo "Hello World from $(hostname -f)" > /var/www/html/index.html
```

Click on Create Launch template>View Launch templates

**Step 3. Select "MyFirstTemplate" Goto Actions>Create Auto Scaling group**

**Step 4. Give name "MyFirstASG" in Auto Scaling group name**
 Click on Next
 
 **Step 5. Network**
 - VPC-default
 - Subnets-Select all the 3 subnets
 
 Click on Next
 
 **Step 5. Load balancing**
 -No Load balancer for as of now
 
 Now Click on Next
 
 **Step 6. Configure group size and scaling policies**
 - Group size
   - Desired capacity-1
   - Minimum capacity-1
   - Maximum capacity-1
   
 - Scaling policies-None
 
 Click on Next
 
**Step 7. Add Notifications**
 Click on Next
 
**Step 8. Add Tags**
 Click on Next
 
**Step 9. Review**
 Click on Create Auto Scaling group
 
**Step 10. Auto Scaling group has been created now goto MyFirstASG>Instances>Lifecycle**
- Status - InService
 
**Step 11. Copy the Instance Ip Address and paste it in Internet browser**

**Step 12. EC2>Auto Scaling groups>MyFirstASG>Edit**

**Step 13. Change Group size**
- Desired capacity-3
- Minimum capacity-3
- Maximum capacity-3

**Step 14. EC2>Auto Scaling groups>MyFirstASG>Instances>Lifecycle**
- See status Pending>InService

**Step 15. Goto EC2 Dashboard>Instances**

Copy the Ip address of all the three Instances one by one and paste it in Internet Browser to see all ec2 instances are running
 
 # End of Lab
 
 
 # Lab8-ASG&ALB
------------------------------------------------------------

**Step 1. Goto AWS Console>All Services>EC2>Load Balancing>Load Balancers>MyFirstALB>Listeners**

**Step 2. Goto EC2>Auto Scaling groups>MyFirstASG>Edit**
- Go to Load Balancers and select the Application or Network Load Balancer target groups
- Select "MyFirstTargetgroup"
- Health check type
  - Select ELB 
  - Put the value to 120 sec of Health check grace period.

Now Click on Update

**Step 3. EC2>Auto Scaling groups>MyFirstASG>Instance management**
- See all instances are InService

**Step 4. Select 1st Instance>Actions>Security>Change security groups**
- Remove "launch-wizard-1" security group
- Add "port80closed" security group
- Click on Save

**Step 5. EC2 Dashboard>Load Balancing>Target Groups>Targets**
- Wait for the Instance to become unhealthy

**Step 6. EC2>Auto Scaling groups>MyFirstASG>Lifecycle**
- See that Instance is Terminating
- Now see that new Instance is launching in place of unhealthy instance

**Step 7. Copy the Newly launched Instance's IP address and paste it in the internet browser**
- It is running 

# End of Lab


# Lab 9--AWS Account SetUp

**Step 1. Open up your browser and type- setting up your AWS free Tier account**

**Step 2. Click on the first result**

**Step 3. Then Click on Create a Free Account**

**Step 4. Provide the following details-**
- Email address
- Password
- Confirm password
- AWS account name

Click on Continue

**Step 5. Now again give some more details-**
- Account type
- Full name
- Company name
- Phone number
- Country/Region
- Address
- City
- State
- Postal code

Click on Create account and continue

**Step 6. Payment Information details-**
- Credit/Debit card number
- Expiration date
- Cardholder's name
- Billing address

**Step 7. Authenticate Transaction with OTP**

**Step 8. Confirm your identity with following-**
- Text message/Voice call
- Country/Region code
- Cell Phone Number
- Security check

Click on Send SMS

**Step 9. Enter verification code**
Click on Verify Code 

**Step 10. Your identity has been verified successfully**
Click on Continue

**Step 11. Select a Support Plan**
- Select Free

**Step 12. Fill the details before it will ask you to sign in to AWS Console**
- My Role is:Academic/Researcher
- I am interested in:Devops

Click on Submit
See Thank You message.

**Step 13. Click on Sign in to the Console**

**Step 14. Sign in page-**
- Provide Root user email address.

Click on Next

**Step 15. Type the password**
Click on Signin

Our Free Tier AWS Acoount is Ready.


# End of Lab

# Lab10
# IAM-User-setup

**Step 1. Login to AWS Console>Click on Your AWS Account>My Billing Dashboard>Billing preferences**

**Step 2. Under Billing Preferences-**
- Select Receive Free Usage Alerts
- Mention Email address
- Select Receive Billing Alerts

Click on Save preferences.

**Step 3. Goto AWS Console>All Services>CloudWatch>Billing**
- Please Switch Region to # US East(N.Virginia) as CloudWatch displays all billing data
and alarms in # US East(N.Virginia)

**Step 4. Billing>Create Alarm>Conditions**
- Threshold type - Static
- Whenever EstimatedCharges is.. - Greater
- than - 5 USD

Click on Next

**Step 5. Configure actions>Notification**
- Alarm state trigger - In alarm
- Select an SNS topic>Create new topic
    - topic name - Default_CloudWatch_Alarms_Topic
	- Provide Email address to receive the notification.
	Click on Create Topic
	
	Now Click on Next
	
**Step 6. Add name and description**
- Alarm name - MyBillingAlarm
- Description

Click on Next

**Step 7. Preview all the details and Click on Create Alarm**
- Successfully created MyBillingAlarm

**Step 8. Goto your Email inbox and look for the email from AWS**
- Open Email and click on Confirm Subscription
- See the message Subscription confirmed

**Step 9. AWS Console>All services>IAM>IAM Dashboard>Users>Add user**
- Set User details-Provide User name
- Select AWS access type 
  - Access Type
     - Programmatic access
     - AWS Management Console access
	 
 - Console password
  
 Click on Next:Permissions
 
 **Step 10. Click on Attach existing policies directly**
 - Select AdministratorAccess
 
 Click on Next:Tags
 
 **Step 11. Click on Next:Review**
 
 **Step 12. Review your choices and Click on Create user**
 
 **Step 13. Click on Download.csv**

# End of Lab

# lab 11
 # IAM user login
 
**Step 1. Signin into AWS Console with Account ID and IAM user name.**

**Step 2. Type the following to change the password at first login-**
- Old password
- New password
- Confirm new password

Click on Confirm password change

**Step 3. Open Amazon Document with following link.**
- https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html

**Step 4. Open your Terminal and type following command with help of above link.**
```sh
$ curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
$ sudo installer -pkg AWSCLIV2.pkg -target /
$ aws --version
```
**Step 5. Follow the link and type command-**
- https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html
```sh
$ aws configure
```
- Provide AWS Access key ID
- Provide Secret Access key
- Default region name
- Default output format

Test the following command to list all the Buckets.
```
$aws s3 ls
```
Now type commands-
```sh
$ cd ~/.aws
$ ls
$ cat credentials
$ cat configure
```

# End of lab

# Lab12
# IAM-lab-part-1

**Step 1. Goto AWS Management Console>All Services>EC2>Auto Scaling>Auto Scaling groups>MyFirstASG>Edit**
- Group size
  - Desired capacity-1
  - Minimum capacity-1
  - Maximum capacity-1
  
 Click on Update
 
**Step 2. Goto AWS Management Console>All Services>IAM**
- Click On Users
- Click on user name Amit>Permissions>AdministratorAccess>Permissions>{}JSON
```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```

**Step 3. Goto IAM Dashboard>Access management>Policies**
- Click on drop down arrow of one policy and see JSON policy.
```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeAddresses",
                "ec2:DescribeByoipCidrs",
                "ec2:DescribeVpcEndpoints",
                "ec2:DescribeVpcs",
                "iam:GetRole",
                "iam:ListRoles",
                "kms:DescribeKey",
                "kms:GetKeyPolicy",
                "kms:ListGrants",
                "kms:ListKeyPolicies",
                "kms:ListKeys",
                "lambda:GetLayerVersionPolicy",
                "lambda:GetPolicy",
                "lambda:ListAliases",
                "lambda:ListFunctions",
                "lambda:ListLayers",
                "lambda:ListLayerVersions",
                "lambda:ListVersionsByFunction",
                "organizations:DescribeAccount",
                "organizations:DescribeOrganization",
                "organizations:DescribeOrganizationalUnit",
                "organizations:ListAccounts",
                "organizations:ListAccountsForParent",
                "organizations:ListAWSServiceAccessForOrganization",
                "organizations:ListChildren",
                "organizations:ListDelegatedAdministrators",
                "organizations:ListOrganizationalUnitsForParent",
                "organizations:ListParents",
                "organizations:ListRoots",
                "s3:GetAccessPoint",
                "s3:GetAccessPointPolicy",
                "s3:GetAccessPointPolicyStatus",
                "s3:GetAccountPublicAccessBlock",
                "s3:GetBucketAcl",
                "s3:GetBucketLocation",
                "s3:GetBucketPolicyStatus",
                "s3:GetBucketPolicy",
                "s3:GetBucketPublicAccessBlock",
                "s3:ListAccessPoints",
                "s3:ListAllMyBuckets",
                "sns:GetTopicAttributes",
                "sns:ListTopics",
                "secretsmanager:DescribeSecret",
                "secretsmanager:GetResourcePolicy",
                "secretsmanager:ListSecrets",
                "sqs:GetQueueAttributes",
                "sqs:ListQueues"
            ],
            "Resource": "*"
        }
    ]
}
```

**Step 4. Goto Ec2 Dashboard and see that Ec2 server is up and running**

**Step 5. Select Instance>Actions>Connect>connect**

**Step 6. Run the following commands**
```sh
$ aws s3 ls
```

# End of lab

# lab13
# IAM-Lab-part-2
**Step 1. IAM Dashboard>Roles>Create Role**
- Select Type of trusted entity
  - AWS Service
- Choose a use case
  - EC2

Click on Next:Permissions

**Step 2. Type s3 in search bar**
- Select AmazonS3FullAccess

Click on Next:Tags
**Step 3. Click on Next:Review**

**Step 4. Provide the Following information-**
- Role name
- Role description

Click on Create role

**Step 5. Role has been created.Attach this IAM role to EC2 instance**
- Select the instance and goto Actions>Security>Modify IAM role>choose IAM role>EC2S3FullAccess

Click on Save.

**Step 6. Now EC2 Dashboard>Select Instance>Actions>Connect>connect**
- type the following command
```sh
$ aws s3 ls
```
Now able to see the s3 details.

**Step 7. Goto AWS Console>All Services>S3>Buckets>teacheramitk>Permissions>Bucket Policy**
```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws-cn:s3:::teacheramitk/*"
            ]
        }
    ]
}
```

**Step 8. IAM Dashboard>Roles>Ec2S3FullAccess>Permissions**
- See JSON Policy for AmazonS3FullAccess

**Step 9. IAM Dashboard>Roles>Ec2S3FullAccess>Trust relationships>Edit Trust Relationship**
```sh
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

# End of lab


# Lab 14
# Vpc-lab-1

**Step 1. AWS Management Console>All Services>VPC(Mumbai Region)**

**Step 2. Following Amazon VPC resources are in Asia Pacific(Mumbai)**
- VPCs - 1
- Subnets - 3
- Route Tables -1
- Internet Gateways - 1
- Nat Gateways - 0
- Network ACLs - 1
- Security Groups - 6
- DHCP options sets - 1
- VPC Peering Connections - 0
- Customer Gateways - 0
- Virtual Private Gateways - 0

Click on Region and change it to US East(N.Virginia) us-east-1

**Step 3. US East(N.Virginia) also has the same Amazon VPC resources**
- Click on Region and change it to US West(Oregon) us-west-2

**Step 4. US West(Oregon) us-west-2 also has the same Amazon VPC resources**

**Step 5. Click on Region and change it to Asia Pacific(Mumbai)**
- Now Click on Subnets 
- 3 Subnets are present
- Select one subnet and click on Route Table Tab
   - It has Two Entries
      - First entry allows access within the VPC
      - Second entry allows outside the VPC

**Step 6. Goto AWS Console>Services>VPC>Route Tables>Routes**
- It has Two Entries
  - First entry allows access within the VPC
  - Second entry allows outside the VPC

**Step 7. Goto AWS Console>Services>VPC>Security>Network ACLs>Subnet associations**
- Acting on all the three subnets
- Inbound Rules - ALLOW ALL
- Outbound Rules - ALLOW ALL

**Step 8. Goto AWS Console>Services>VPC>Security>Security Groups**
- Select Default security group>Inbound Rules
  - Accepts traffic from an Ec2 instance with the same Security Group

**Step 9. Goto AWS Console>Services>VPC>Internet Gateways**  
- 1 Internet Gateway attached to Default VPC

# End of lab

# lab 15

# Vpc-Lab-2

**Step 1. Goto AWS Console>Services>VPC>Create VPC**
- Provide the following details
  - Name - CustVPC
  - IPv4 CIDR block - 10.0.0.0/16
  
 Click on Create VPC

**Step 2. VPC has been created successfully**

**Step 3. Goto VPC>Subnets>Create Subnet**
Give following details
- VPC ID - default vpc
- Subnet name - PubSub
- Asia Pacific(Mumbai)/ap-south-1a
- IPv4 CIDR block - 10.0.1.0/24

Click on Create Subnet

**Step 4. Goto VPC>Subnets>Create Subnet**
Give following details
- VPC ID - CustVPC
- Subnet name - PvtSub
- Asia Pacific(Mumbai)/ap-south-1b
- IPv4 CIDR block - 10.0.0.0/24

Click on Create Subnet

**Step 5. Goto AWS Console>Services>VPC>Route Tables**
- Click on CustVPC route table and rename it to "DefRTCustVPC"

**Step 9. Goto AWS Console>Services>VPC>Internet Gateways>Create Internet Gateway**
Create route table**
Provide the details-
- Name - CustRTCustVPC
- VPC - CustVPC

Click on Create

**Step 9. Goto AWS Console>Services>VPC>Internet Gateways>Create Internet Gateway**
- Give Name - CustVPCIG

Click on Create Internet Gateway

**Step 10. Goto AWS Console>Services>VPC>Internet Gateways>CustVPCIG>Actions>Attach to VPC**
- Select CustVPC
- Attach Internet Gateway

**Step 11. Goto AWS Console>Services>VPC>Route Table>DefRTCustVPC>Routes**
- It has one entry that allows any access within the VPC


**Step 12. Goto AWS Console>Services>VPC>Route Table>CustRTCustVPC>Routes**
- It has one entry that allows any access within the VPC

**Step 13. Goto AWS Console>Services>VPC>Route Table>DefRTCustVPC>Subnet associations**
- No Subnet association

**Step 14. Goto AWS Console>Services>VPC>Route Table>CustRTCustVPC>Subnet associations**
- No Subnet association

**Step 15. Goto AWS Console>Services>VPC>Route Table>CustRTCustVPC>Subnet associations>Edit subnet associations**
- Select PubSub

 Click on Save.

- Now CustRTCustVPC is associated with PubSub 

**Step 16. Goto AWS Console>Services>VPC>Route Table>CustRTCustVPC>Routes>Edit routes>Add route**
Give the following details.
- Destination - 0.0.0.0/0
- Target - Internet Gateway

Click on Save routes and click on Close

**Step 17. Goto VPC>Subnets>PubSub>Actions>Modify auto-assign IP settings**
- Select "Enable auto-assign public IPv4 address"

Click on Save

Now Auto-assign public IPv4 address has YES entry.

# Lab 16
VPC-Lab-3

**Step 1. Goto AWS Console>Services>EC2>EC2 Dashboard>Instances>Launch Instances**
- Select Amazon Linux2 AMI
- Select Instance type - t2.micro

Click on Next:Configure Instance Details

**Step 2. Provide the following details-**
- Select CustVPC 
- Select Subnet - PubSub
- Auto-assign Public IP - Use subnet setting (Enable)
- Advanced details>User Data
```sh
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd.service
systemctl enable httpd.service
echo "Hello World from $(hostname -f)" > /var/www/html/index.html
```

Click on Next:Add Storage

**Step 3. Click on Next:Add Tags**

**Step 4. Click on Next:Configure Security Group**
- Create a new security group
- Click on Add rule
  - Type - HTTP
  - Protocol -TCP
  - Port - 80
  - Source - Custom-0.0.0.0/0
  
Click on Review and Launch>Launch

**Step 5. Choose an existing key pair>Select key pair**

Click on Launch Instances


**Step 6. Goto EC2 Dashboard>Instances>Launch Instances**
- Select Amazon Linux2 AMI
- Select Instance type - t2.micro

Click on Next:Configure Instance Details

**Step 7. Provide the following details-**
- Select - CustVPC 
- Select Subnet - PvtSub
- Auto-assign Public IP - Use subnet setting (Disable)
- Advanced details>User Data
  - No need for Web server

Click on Next:Add Storage

**Step 8. Click on Next:Add Tags**

**Step 9. Click on Next:Configure Security Group**
- Select an existing security group

  
Click on Review and Launch>Launch

**Step 10. Choose an existing key pair>Select key pair**

Click on Launch Instances

**Step 11. Goto EC2Dashboard>Instances**
- Select the Public Instance
  - Copy the Public IPv4 address
  - Paste it in the Browser
  - Public Server is accessible

**Step 12. EC2Dashboard>Public instance>Actions>Connect>connect**
- We are into EC2 server
  - Ping google.com and see the success.
  
**Step 13. EC2Dashboard>Private instance** 
- No Public Ipv4 address

# End of Lab
  



# lab17
# s3-lab

**Step 1. AWS Management Console>All Services>S3>Create Bucket**
- Provide globally unique Bucket name - "teacheramitk"
- Region
- Block all public access - leave as for now
- Bucket versioning - leave as for now

Click on Create Bucket.

**Step 2. Click on created Bucket "teacheramitk"**
- Click on Upload

**Step 3. Upload>Add Files**
- Select file "testfile1.txt" to upload

Upload scucceeded

**Step 4. Click on this Object**
- In Details Click on Object URL
  - Access denied error (Because object is not public)

**Step 5. Amazon S3>teacheramitk>Permissions>Edit Block public access**
- Uncheck Block all public access
- Click on Save changes
- type confirm and click on confirm

**Step 6. Amazon S3>teacheramitk>object"testfile1.txt">Object actions>Make public>Click Make public**
- successfully edited public access

**Step 7. Now Click on Object URL**
- File is accessible now

**Step 8. Amazon S3>teacheramitk>Permissions>Bucket policy>Edit**
```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::teacheramitk/*"
            ]
        }
    ]
}
```

Click on Save changes

**Step 9. Goto Amazon S3>teacheramitk>Upload**
- Add files "testfile2.txt"
- Click on Object URl of "testfile2.txt"
- file is accessible

**Step 10. Amazon S3>teacheramitk>Properties>Bucket Versioning>Edit>Enable**
- Click on Save changes

**Step 11. Goto Amazon S3>teacheramitk>Objects>Upload>Add files**
- Select "testfile3.txt"
- Click on Upload
- Click on "testfile3.txt"
- Click on Object URL
- File is accessible

**Step 12. Try to Upload different version of same file**
- Goto Amazon S3>teacheramitk>Objects>Upload>Add files
- Secret version 2 of "testfile3.txt"
- Click on Upload
- Click on "testfile3.txt"
- Click on Object URL
- File is accessible
- Amazon S3>teacheramitk>"testfile3.txt">Versions
- Note the upload timings of different versions

**Step 13. Open AWS CLI Terminal**
```sh
$ aws s3 ls
```
- Above command shows the name of bucket in output.

# lab-18
# VSCode-install-Lab

**Step 1. Open Internet Browser and type "install visual studio code" in google search**

**Step 2. Click on the very first link**

**Step 3. Select your Operating system link**
- As soon as you click on link it will start downloading vscode zip file

**Step 4. Goto Downloads>VSCode-drawin-stable.zip>RightClick>open with>Archive Utility**

**Step 5. File is Unzipped**

**Step 6. Now Move content to Application folder**

**Step 7. Goto Applications and click on VSCode icon to access it**

# End of lab


		   		  
# lab-19
# # CloudWatch-Alarm-Lab-1

**Step 1. Launch Ec2 Instance**
- Goto AWS Management Console>Services>EC2>EC2 Dashboard>Instances>Launch Instances
- Select Amazon Linux2 AMI
- Select Instance type - t2.micro

Click on Next:Configure Instance Details

**Step 2. Keep details default**

Click on Next:Add Storage

**Step 3. Click on Next:Add Tags**

**Step 4. Click on Next:Configure Security Group**
- Select an existing security group

  Click on Review and Launch>Launch

**Step 5. Choose an existing key pair>Select key pair**

- Click on Launch Instances

**Step 6. Goto EC2Dashboard>Instance>Monitoring**
-Wait for sometime for Metrics to be created

**Step 7. Goto AWS Management Console>Services>CloudWatch>Metrics>All metrics>EC2>Per-Instance Metrics** 
- Copy the instance-id from EC2 Dashboard
- Paste it in the Per-Instance Metrics Search bar
- Select the CPUUtilization Metric in drop-down menu

**Step 8. Goto AWS Management Console>Services>CloudWatch>Alarms>Create alarm**
- Select Metric for alarm
  - All metrics>per-Instance Metrics
  - Copy the instance-id from EC2 Dashboard
  - Select the CPUUtilization Metric in drop-down menu
Click on Select Metric

**Step 9. Specify metric and conditions**
- Change Period - 1 minute
- Conditions - Static
  - Whenever CPUUtilization is ... - Lower
  - Than... threshold value - 40 percent
 
Click on Next

 **Step 10. Now Configure actions>Notification - Click on Remove (As We are using EC2 action Below)** 
- EC2 action>Add Ec2 action
  - Alarm state trigger
    - In Alarm
	  - Take the following action
	    - Select Stop the instance
		
Click on Next

**Step 11. Add name and description**
- Alarm name - MyFirstAlarm

Click on Next

**Step 12. Preview and create**
- see step2:configure actions

Click on Create alarm

**Step 13. CloudWatch>Alarms>MyFirstAlarm**
- Showing insufficient data (Wait for some time)
- See in EC2Dashboard instance is running fine
- Check it after some time Instance is stopped now.

CPUUtilization was below 40 percent and CloudWatch stopped it.


# End of lab

# Lab 20
# CloudWatch-lab-2

**Step 1. Goto AWS Management Console>Services>Simple Notification  Service>Create topic**
- Give name - MyFirstTopic

Click on Next Step

**Step 2. Create Topic>Details>Standard**
- Keep everthing default

Click on Create Topic

**Step 3. Goto AWS Management Console>Services>Amazon SNS>Subcriptions>Create subscription**
- Details
  - Topic ARN - selct MyFirstTopic
  - Protocol - Email
  - Endpoint - teacheramitk@gmail.com
  
Click on create subscription

**Step 4. Amazon SNS>Topics>MyFirstTopic>Subcriptions**
- Pending confirmation
- Check the Email given above
- See the Email from AWS Notification-Subcription Confirmation
  - Click on Confirm subscription
  - See the confirmation 

**Step 5. Amazon SNS>Subcriptions**
- See that status is Confirmed of Topic MyFirstTopic

**Step 6. CloudWatch>Events>Rules>Create Rule**
In Event Source -
- Select - Event Pattern
  - Service Name - Ec2
  - Event Type - EC2 Instance-change Notification
  - Specific state(s)
    - Select - running
	
  - Specific Instance id(s) 
    - Copy Instance id from EC2Dashboard 

Than Targets>Add Targets>SNS topic>MyFirstTopic

Click on Configure details.

**Step 7. Configure rule details**
- Name - MyFirstEvent

Click on Create rule.

**Step 8. Goto AWS Management Console>Services>EC2>EC2 Dashboard>Instances**
- Select the Instance>Instance state>Start the Instance
  - CloudWatch will send the notification to SNS Topic
  - Check for Notification in Email inbox
 
 # End of lab

# Lab 21
# DynamoDb-Lab

**Step 1. Goto AWS Management Console>Services>DynamoDB>Create Table**
- Give Table name - Movies
- Primary key 
  - Partition key- Year
    - Number
  - Add sort key -title
    - String
- Table settings
  - uncheck default settings 	
  - Read/Write capacity mode - Provisioned 
  - Provisioned capacity 
    - Read capacity - 1
	- Write capacity - 1
  - Auto Scaling
    - uncheck Read capacity and write capacity
-Encyrption at Rest - default

Click on Create 

**Step 2. TABLE Created successfully**
- Goto Movies>Items>create item
- Provide the following values:
  - Year - 1997
  - title - As good as it gets
 
 Click on Save
 
 **Step 3. Goto Movies>Items>create item**
 - Provide the following values:
 - year - 2020
 - title - test1
 - Click on +
    - Append>string
      - genre String:romcom
 
 Click on save
 
 **Step 4. Goto Movies>Items>create item**
 - Provide the following values:
 - year - 1997
 - title - Titanic
 - Click on +
   - Append>Number
     -rating Number: - 9

 Click on Save
 
 **Step 5. Goto Movies>Items>select 1997>Actions>Edit**
 - Click on +
 - Append>Number
 - Give value rating to Number - 9
 
 Click on Save
 
 **Step 6. Goto Movies>Items>1997>Actions>Delete>Delete**
 
 **Step 7. Goto Movies>Items>Select from drop-down>Query**
 - Provide the following values:
 - Partition key 1997
 - Sort key - As good as it gets
 
 **Step 8. Goto Movies>Delete Table>delete**
 - Table has been deleted

# End of lab
 
 
 # lab 22
 # nodejs-lab
 
 **Step 1. Open google in Internet Browser and type "install node js on mac"**
 
 **Step 2. Click on Very first link "Download | Node.js"**
 
 **Step 3. Downloads>LTS version>macos installer**
 - Download has been started
 
 **Step 4. Open downloaded file Install Node.js**
 
 **Step 5. Click on Continue>continue>Agree>Install**

 **Step 6. Give User name and Password**

**Step 7. Click on Install Software**

**Step 8. Click on Install**

**Step 9. Click on Close**
 
**Step 10. Open Terminal**
```sh
$ node -v
```

# End of lab

# Lab 23 
# Clean_Up-Lab

**Step 1. AWS Management Console>EC2 Dashboard>Auto Scaling Group**
- Ensure that all the ASG group have following settings by Editing-
  - Desired - 0
  - Minimum - 0
  - Maximum - 0
  
**Step 2. AWS Management Console>EC2 Dashboard>Auto Scaling Group>MyFirstASG>Delete**
 - Type delete to confirm
 - Click on delete
  
**Step 3. AWS Management Console>EC2 Dashboard>Load Balancing>Target groups>MyFirstTargetGroup>Actions>Delete**
- Click YES,Delete
- Error saying that it is in use by listener or rule

**Step 4. AWS Management Console>EC2 Dashboard>Load Balancing>load Balancers>MyFirstALB>Actions>Delete**
- Click on Yes,Delete

**Step 5. AWS Management Console>EC2 Dashboard>Load Balancing>Target groups>MyFirstTargetGroup>Actions>Delete**
- Click on Yes,Delete  

**Step 6. AWS Management Console>EC2 Dashboard>Instances**
- Select the running instances>Instance state>Terminate instance
- Click on Terminate

**Step 7. AWS Management Console>Services>ElasticBeanStalk>Applications>MyFirstEbsApp>Actions>Delete Application**
- Enter the name in Confirm Application Deletion
- Click on Delete
- Note All the resources apart from S3 Bucket that application deployment had created, will be deleted

# End of Lab























