# Lab1

Ec2 Lab With Manual Apache
------------------------------

# Goto AWS Management Console>AWS Services>Find services>Type EC2>Click on EC2>EC2 Dashboard>Instances>Launch Instances

**Step 1.Choose AMI(Amazon Machine Image) Amazon linux 2 AMI Free tier eligible,Click to Select**

**Step 2.Choose Instance type**
 - Type t2.micro Free tier 
 - vCPUs-1 
 - Memory-1Gib

Click on Next-Configure Instance details

**Step 3.Configure Instance details**
- Number of Instances- type 1
- Network-Default VPC
- Subnet- No preference
- Auto assign Public IP-Use Subnet setting (Enable)
- IAM Role
- User Data

  Click on Next:Add Storage

**Step 4.Next Add Storage**
- Keep Default Size-8 Gib

  Click Next:Add Tags

**Step 5 ADD Tags**
  Leave as of now
  
  Click on Next:Configure Security Group

**Step 6.Configure Security Group**
 -SSH already there
 -Add Rule for HTTP

Click Review and Launch >Launch

**Step 7. Review**
Select an existing key pair or create a new key pair

- Select create a new pair
- Provide key pair name
- Click on Download key pair 
- Launch instance

**Step 8. Click on the launched Instance and Click on Details to see the Public IP and other details.**

**Step 9. Ec2 dashboard>Instances>Launched Instance>Actions>Connect**

**Step 10. Login as Superuser**

```sh
$ sudo su
```

**Step 11. Run the Following Commands.**
```
$ yum update -y
$ yum install -y httpd
$ systemctl start httpd.service
$ systemctl enable httpd.service
$ echo "Hello World from $(hostname -f)" > /var/www/html/index.html
```


```
$ cd /var/www/html
$ ls -a
$ echo "Hello World from $(hostname -f)" > /var/www/html/index.html
$ ls -a
$ cat index.html
```
**Step12 Copy the Public IP and paste in the browser to see Apache Web server is Running**

### End Of Lab




