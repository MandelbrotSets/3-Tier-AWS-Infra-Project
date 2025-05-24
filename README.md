AWS Three Tier Web Architecture Console Build
Description:

This workshop is a hands-on walkthrough of a three-tier web architecture created in AWS. The plan is to manually creating the necessary network, security, web, app, and database components and configurations in order to run this architecture in a highly available, fault tolerant and scalable manner.


In this architectured infrastructure we will have a public-facing Application Load Balancer forwarding client traffic to our web tier EC2 instances. The web tier will be running Nginx webservers that are configured to serve a React.js website and redirects our API calls to the application tier’s internal facing Load Balancer. The internal facing Load Balancer then forwards that traffic to the application tier, which is written in Node.js. The application tier manipulates data in an Aurora MySQL multi-AZ database and returns it to our web tier. Load balancing, health checks and autoscaling groups are created at each layer to maintain the availability of this architecture.


AWS Steps:
Create 3 Tier Architecture & Integrating Other AWS Resources

Step 1: Download Code from GitHub in Your Local System

Step 2: Create Two S3 Buckets
One S3 bucket for storing web-server & app-server code.
Upload the code to your S3 from your local system.
The other S3 bucket will store VPC flow logs.

Step 3: Create an IAM Role with these policies
S3 read only.
SSM managed instance core.
Name it and save it

Step 4: Create VPC, Subnets, IGW, NAT-GW, RT
Enable auto-assign public IP for web-tier public subnets.
Create flow logs for VPC & use the S3 bucket created above.

Step 5: Create Security Groups
External-Load-Balancer-SG HTTP (80): 0.0.0.0/0.
Web-Tier-SG HTTP pointing to Ext-LB-SG.
Internal-Load-Balancer-SG HTTP pointing to Web-Tier-SG.
App-Tier-SG Port 4000 pointing to Internal-LB-SG.
DB-Tier-SG MySQL (3306) pointing to App-Tier-SG.

Step 6: Create DB Subnet Group & RDS
Create DB subnet group in RDS
Create RDS - Multi-AZ.
Place them in DB subnet group created above.

Step 7: Create Test App Server, Install Packages, Test Connections
Test App-Server Commands
Create AMI.
Create launch template using AMI.
Create target group for load balancer
Create internal load balancer.
Create autoscaling group.
Edit nginx.conf file in local system by adding Internal-LB-DNS & upload the file in S3.

Step 8: Create Test Web Server, Install Packages (Nginx, Node.js (React)), Test Connections
Test Web-Server Commands
Create AMI.
Create launch template using AMI.
Create target group.
Create external load balancer.
Create autoscaling group.

Step 9: Add External-ALB-DNS Record in Route 53
Step 10: Create CloudWatch Alarms Along with SNS
Step 11: Create CloudTrail

Step 12: Deleting the Entire Infrastructure
Delete CloudFront.
Delete CloudWatch alarms.
Delete records from Route 53.
Delete load balancers, target groups, ASG, launch templates.
Delete security group.
Delete NAT gateway (it will take 5 mins).
Release elastic IP.
Delete VPC.
Delete RDS subnet group, RDS.

Workshop Instructions:
See AWS Three Tier Web Architecture
