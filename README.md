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
  => then why the heck you want it in one month. \(T^T)/

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

### EC2 Instance Types

#### General Purpose - t tier

- Great for a diversity of workloads such as web servers or code repositories
- Balance between:
  ..- Compute
  ..- Memory
  ..- Networking
- In the course, we will be using the t2.micro which is a General Purpose EC2 instance

#### Compute Optimized - c tier

- Great for compute-intensive tasks that require high performance processors:
- Batch processing workloads
- Meida transcoding
- High performance web servers
- High performance computing (HPC)
- Scientific modeling & machine learning
- Dedicated gaming servers

#### Memory Optimized - m tier

- Fast performance workloads that process large data sets in Memory
- Use cases:
  ..- High performance, relation/non-relation databases
  ..- Distributed web scale cache stores
  ..- In-memory databases optimized for BI (business intelligence)
  ..- Applications performing real-time processing of big unstructured data

#### Storage Optimized - i tier

- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- Use cases:
  ..- High frequency onlikne transaction processing (OLTP) systems
  ..- Relational & NoSQL databases
  ..- Cache for in-memory databases (for example, Redis)
  ..- Data warehousing applications
  ..- Distributed file systems

#### Security Groups

- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of the EC2 instnaces
- Security groups only contain allow rules
- Security groups rules can reference by IP or by security group

- Acting as a "firewall" on EC2 instances
- They regulate:
  ..- Access to ports
  ..- Authoried IP ranges - IPv4 and IPv6
  ..- Control of inbound network (from toher to the insatnce)
  ..- Control of outbound network (from the instance to other)

- Can be attatch to multiple instances
- Locked down to a region / VPC combination

### Purchasing Options

- On-Demand Instances -- short workload, predictable pricing, pay by second
- Reserved (1 & 3 years)
  ..- Reserved Instances - long workloads
  ..- Convertible Reserved Instances - long workloads with flexible instances
- Savings Plans (1 & 3 years) -- commitment to an amount of usage, long workloads
- Spot Instances -- short workloads, cheap, can lose instances (less Reliable)
- Dedicated Hosts -- book an entire physical server, control instance placement
- Dedicated Instances -- no other customers will share your hardware
- Capacity Reservations -- reserve capacity in a specific AZ for any duration

#### On Demand

- Pay for what you use:
  ..- Linux or Windows - biling per second, after the first minute
  ..- All other operating systems - billing per hour
- Has the highest cost but no upfront payment
- No long-term commitment
- Recommended for **short-term** and **un-interrupted** workloads, where you can't predict how the application will behave

#### Reserved Instances

- Up to 72% discount compared to On-demand
- You reserve a specific instance attributes ( Instance Type, Region, Tenacy, OS)
- Reservation Period -- 1 Year (+discount) or 3 years (+++discount)
- Payment Options - No Upfront(+), Partial Upfront (++), All upfront (+++)
- Recommended for steady-state ussage applications (think database)
- You can buy and sell in the Reserved Instance Marketplace

- Convertible Reserved Instance
  ..- Can change the EC2 instance type, instance family, OS, scope and tenancy
  ..- Up to 66% discount

#### Savings Plans

- Get a discount based on long-term usage (up to 72% - same as Reserved)
- Commit to a certain type of usage (\$10/hour for 1 or 3 years)
- Usage beyond EC2 Saving Plans is billed at the On-Demand price
- Locked to a spacific instance family & AWS region (e.g., M5 in us-east-1)
- Flexible across:
  ..- Istance Size (e.g., m5.xlarge, m5.2xlarge)
  ..- OS (e.g., Linux, Windows)
  ..- Tenancy (Host, Dedicated, Default)

#### Spot Instance

- Can get discount of up to 90% compared to On-Demand
- Instances that you can "lose" at any point of time if your max price is less than the current spot price
- The MOST cost-efficient instances in AWS

- Useful for workloads that are resilient to failure
  ..- Batch jobs
  ..- Data analysis
  ..- Image processing
  ..- Any distributed workloads
  ..- Workloads with flexible start and end time

- Not suitable for critical jobs or databases

#### Dedicated Hosts

- A Physical server with EC2 instance capacity fully dedicated to your use
- Allows you addresss compliance requirements and use your existing server-bound software licenses (per-socket, per-core, pe--VM software licenses)
- Purchasing Options:
  ..- On-Demand - pay per second for active Dedicated Host
  ..- Reserved - 1 or 3 years (No Upfront, Partial Upfront, all Upfornt)
- The most expensive option
- Useful for software that have complicated licensing model (BYOL - Bring Your Own License)
- Or for companies that have strong regulatory or compliance needs

#### Dedicated Instances

- Instances run on hardware that's dedicated to you
- May share hardware with other instances in same account
- No control over instance placement (can move hardware after Stop / Start)

#### Capacity Reservations

- Reserve On-Demand instances capacity in a specific AZ for any duration
- You always have access to EC2 when you need it
- No time commitment ( create/ cancel anytime), no billind discoutns
- Bomcine with Regional Reserved Instances and Savings Plans to benefit from billind discounts
- You're charged at On-Demand rate whether you run instances or not
- Suitable for short-term uninterrupted workloads that neesd to be in a specific AZ

## Spot Instance Requests

- Can get a discount of up to 90% compared to On-demand
- Define **max spot price** and get the instance while **current spot price** < max
  ..- The hourly spot price vaires based on offer and capacity
  ..- If the current spot price > your max price you can choose to **stop** or **terminate** your instance with a 2 minutes grace period

- Used for batch jobs, data analysis, or workloads that are resilient to failures

### How to terminate Spot instances

To use Spot Instances, you need to create Spot instance request that includes:

- Desired number of instances
- Instance type
- Availability zone
- Maximum price that you are willing to pay per instance hour

```




                                                           Start                       Stop
                                         .--------------(persistent)<------------- (persistent)
                                         |
                                         |                Interrupt                      ^
                                         |    .----------(persistent)<-----------------. |
                                         |    |                                        | |
                                         |    |                                        | |
                                         |    |                                        | |
                                         v    v                                        | |
                      .-------------------------------------.                          | |
                      |            SPOT REQUEST             |                          | |
                      |                                     |                       .---.
                      | Maximum price                       |      Lauch            | .---.
                      | Desired number of instances         |------instances---->   '-| .---.
Create Request------->| Launch specification                |                         '-|   |
                      | Request type: one-time | persistent |                           '---'
                      | Valid from, valid until             |                           |
                      |                                     |                           |
                      '-------------------------------------'                           |
                                         |                                              |
                                         |                                              v
                                         |                                         Interrupt
                                         |                                         (one-time)
                                         v
                                  Request Failed

```


If you want to cancel the spot request, It's need to be in **open, active, or disabled**

- Spot instance will not be terminate. I have to terminate it myself. Event if I cancel the spot request. The instance will still be running and need manual termination
- Not AWS responsibility to terminate them


First is to cancel the spot request -> then terminate the instances

Or else the instance will be create because **spot request** detect that the replicas have not met


### Spot fleets
- Spot fleets = set of Spot Instances + (optional) On-Demand instances
- The spot Fleet will try to meet the target capacity with price constrains
..- Define possible launch pools: instance type (m5.large), OS, Avaialbility Zone
..- Can have multiple launch pools, so that the fleet can choose
..- Spot fleet stops launching istnaces when reaching capacity or max cost
- Strategies to allocate Spot Instances:
..- LowestPrice: from the pool with the lowest price (cost optimization, short workload)
..- diversified: distributed across all pools (great for availability, long workloads)
..- capacityOptimized: pool with the optimal capacity for the number of instances

- Spot fleet allow us to automatically request Spot Instances with the lowest price


#### Spot lab
- pricing history
- request spot instance
..- Manual configure
..- Use a launch template


## Networking ~ yay

This is the part in my knowledge that I least certain, and I want to understand it better

