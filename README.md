# AWS-SAA-C02 study notes

Goal: I want to get the cert in one month

- I have experience with AWS, and have access to resources to test and do hand-on
- I have strong experience with linux
- I have strong experience with docker
- I have strong experience with k8s
- ~~I know vim, vim will speed up the process 300%~~

Weakness:
- I'm not very good at networking, knowing the basic, still not get the NAT and the DHCP, CIDR block...
..- I understand port
..- I understand tcp, inbound, outbound connection. 

NAT gateway if don't know how to use will cost you fortune on aws 

- Slow learner, have to reread a lot and take a lot of notes to understand
=> then why the heck you want it in one month.  \(T^T)/


## IAM 

- Users Group
- Users
- Policies
- Roles
- Security tools
..- Credential Report (Account level)
..- Access Advisort (User level)
- aws cli


### IAM Guildelines & best practices
- Don't use the root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions to groups
- Create a strong password policy
- User and enforce the user of Multi Factor Authentication (MFA)
- Create and use Roles for giving permission to AWS services
- Use Access Keys for Programmatic Access (CLI/SDK)
- Audit permissions of your account with the IAM Credentials Report
- Never share IAM users & Access Keys

## Fundamentals

### Amazon ec2

- EC2 is one of the most popular of AWS's offering
- EC2 = Elastic Compute Cloud = Infrastructure as a Service
- It mainly consists in the capability of:
..- Renting virutal machines (EC2)
..- Storing data on virtual drives (EBS)
..- Distributing load across machines (ELB)
..- Scaling the services using an auto-scaling group (ASG)

### EC2 sizing & configuration options
- OS: linux, windows or MacOS
- how much computer power & cores (CPU)
- how much random-access memory (RAM)
- How much storage space:
..- Network-attached (EBS & EFS)
..- Hardware (EC2 instance store)
- Network card: speed of the card, Public IP Address
- Firewall rules: security group
- Bootstrap script (configure at first launch): EC2 User Data

EC2 User Data
- It is possible to bootstrap our instances using an EC2 User data script.
- bootstraping means lauching commands when a machine starts
- That script is only run once at the instance first start
- EC2 User dat ais use dto automate boot tasks such as:
..- Installing updates
..- Installing software
..- Downloading common files from the internet

- EC2 User Data Script runs with the root user
