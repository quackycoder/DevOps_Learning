## 1.EC2

### --> How to create EC2 Instance?

### --> What is AMI?

### --> How to choose right AMI for creating Instance?

### --> How to secure EC2?

### --> How to take automated backups?

### --> How to migrate your instance from one Region to another and one account to another?

### --> How can you recover keys of an EC2 Instance?

### --> If everything seems okay but still you are not able to login to EC2 how will you check it?

### --> How do you choose right type of EC2 instance?

## 2.EBS

### --> How many types of EBS volumes are there?

### --> How to take backup of a volume?
### --> Can I associate one EBS to more than 1 instance?
### --> What are the conditions if we need to mount EBS to instance?
### --> What is maximum size of EBS Volume?
### --> Where EBS snapshots are stored?

## 3.S3

### --> What is S3?

### --> How to host a website with S3?

### --> What is the use of multipart upload?

### --> How many S3 buckets can you create in your account?

### --> What is default size of S3 Bucket?

## 4.VPC

### --> What is VPC?

### --> What is CIDR which VPC supports?

### --> How does VPC peering work?

### --> What is DHCP and DNS options available in VPC?

### --> What is VPC Flow Logs?

### --> Why do we use NACL with VPC?

## 5.IAM

### --> What is IAM?

### --> What is more secure IAM user OR IAM role?

### --> How to create custom IAM policy?

### --> How do you manage password policy for IAM Users?

### --> What will you do if you want to an IAM user to reset password at next login?

### --> How do you rotate Access key of IAM users?

### --> How do you enable MFA with IAM users?

### --> What are the supported Devices by AWS MFA?

### --> How many rules can I associate with 1 IAM user by default?

## 6.AUTOSCALING

### --> What is autoscaling group?

### --> How does auto scaling work?

### --> What is end point for autoscaling health check?
### --> How does autoscaling manage traffic flow for ELB?

### --> If I want to launch multiple type of instance with in same target group what will I need to do?

### --> Can I use spot and on-demand instance with autoscaling group?

### --> Can I associate multiple targets group under one autoscaling group?

### --> Can I associate target groups created in different VPCs?

## 7.ELB

### --> What is ELB in AWS?
### --> What are different types of ELB in AWS?

### --> What is main difference between Application and Network ELB?

### --> How do you select between Application and Network ELB to use for your application?

### --> How do you manage host and path based routing with App ELB?

### --> What rule will you implement if you need to forward all traffic coming form a single application to any specific target group?

### --> Can I forward traffic based on source IP address?
### --> What is provisioned ELB?
### --> How many IP address do we get with ELB?

### --> What happens if ELB goes down?

### --> How many rules can I attach to one ELB?
### --> How many conditions can I attach per rule?

## 8.CLOUDWATCH

### --> How to you monitor services with Cloud Watch?

### --> What is default metric of Cloud watch?

### --> Can I monitor applications running on EC2 instance?

### --> How can I set alarms with CloudWatch?

### --> Can I monitor resource by CloudWatch in multiple regions?

## 9.CLOUDFORMATION

### --> What is cloud formation?

### --> How do you provision Infra with CloudFormation?

### --> Can we provision replica of existing environment with CloudFormation?

### --> What are the limitation of CloudFormation?

## 10.CLOUDTRAIL

### --> What is use of CloudTrail?

### --> Where can I check activities performed by IAM users?

### --> How to track activities of IAM admins?

### --> How can I check that if an EC2 instance is created, who created it?

### --> Can I monitor activity of IAM user of single region or multiple regions?

### --> Where logs are stored for CloudTrail?

## 11.CLOUDFRONT

### --> What are 2 main components of CloudFront?

### --> What is Origin in CloudFront?

### --> What is the use of distribution setting?

### --> What headers does cloud front cache by default?

### --> How to implement ssl certificate with CloudFront?

### --> How can I generate private url with help of CloudFront?

### --> How do I user WAF and Shield with CloudFront?

### --> What are the protocol does CloudFrom Support?

### --> What type of distribution does CloudFront Support?

### --> How can I clear cache of an object in CloudFront?

### --> Can I terminate HTTP to HTTPS using CloudFront?

##12.LAMBDA

### --> What is Lambda?

### --> How do you use lambda in your current project?

### --> How can you schedule a task using lambda?

### --> How will you write a lambda function to stop and start EC2 instance?

### --> Can we get notification with Lambda if an object is missed in S3 bucket?

### --> How can lambda help in cost optimisation?

### --> What are the use-cases where you have used lambda?

## 15.RDS

### --> What is RDS?

### --> How many DB engine does AWS support?

### --> What are the conditions to enable/create read replica of MYsql DB?

### --> Can I create read replica of a read replica?

### --> How can I restore Data from Automated Created Snapshot?

### --> What type of rules can we have with RDS?

### --> How do you secure RDS?

### --> What are options group?

## 16.ROUTE53

### --> What is Route53?

### --> How do you host your domain with Route53?

### --> What type of records are supported by Route53?

### --> How many type of zone can we host in Route53?

### --> Can I associate multiple VPCs with single hosted zone?

### --> Can I forward traffic to Internal ELB form Public hosted zone?

### --> Can I use CloudFront as an A record with Route53?
