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
