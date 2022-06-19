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

### Placement Groups

- Sometimes you want control over the EC2 Instance placement strategy
- That strategy can be defined using placement groups
- When you create placement group, you specify one of the following strategies for the group:
  ..- Cluster -- clusters instances into a low-latency group in a single Availability Zone
  ..- Spread --spreads instances across underlying hardware (max 7 instances per group per AZ) -- critical applications
  ..- Partition -- spreads instances across many different partitions (which rely on different sets of racks) with an AZ. Scales to 100s of EC2 instances per group (Hadoop, Cassandra, Kafka)

#### Cluster

```
  .-----------------------------------------------------.
  |                                                     |
  |                                                     |
  |                  .-----.      .-----.      .-----.  |
  |                  | EC2 |------| EC2 |------| EC2 |  |
  |                  '------.   . '-----'-.  .-------'  |
  |                     .    \ /     .     \/     .     |
  |  Same Rack          |     /      |     /\     |     |
  |  Same AZ            '    / \     '    /  \    '     |
  |                  .-----.'   ' .-----.'    '.-----.  |
  |                  | EC2 |------| EC2 |------| EC2 |  |
  |                  '-----'      '-----'      '-----'  |
  |                                                     |
  |                                                     |
  '-----------------------------------------------------'
```

- Pros: Great network (10 Gbps bandwidth between instances)
- Cons: If the rack fails, all instances fails at the same time
- Use case:
  ..- Big Data job that needs to complete fast
  ..- Application that needs extremely low latency and high network throughput

#### Spread

```
  .---------------------.     .---------------------.    .---------------------.
  |     us-east-1a      |     |     us-east-1b      |    |     us-east-1c      |
  |                     |     |                     |    |                     |
  |  .---------------.  |     |  .---------------.  |    |  .---------------.  |
  |  | .-----------. |  |     |  | .-----------. |  |    |  | .-----------. |  |
  |  | |           | |  |     |  | |           | |  |    |  | |           | |  |
  |  | |    EC2    | |  |     |  | |    EC2    | |  |    |  | |    EC2    | |  |
  |  | |           | |  |     |  | |           | |  |    |  | |           | |  |
  |  | '-----------' |  |     |  | '-----------' |  |    |  | '-----------' |  |
  |  |               |  |     |  |               |  |    |  |               |  |
  |  |   Hardware 1  |  |     |  |   Hardware 3  |  |    |  |   Hardware 5  |  |
  |  '---------------'  |     |  '---------------'  |    |  '---------------'  |
  |                     |     |                     |    |                     |
  |  .---------------.  |     |  .---------------.  |    |  .---------------.  |
  |  | .-----------. |  |     |  | .-----------. |  |    |  | .-----------. |  |
  |  | |           | |  |     |  | |           | |  |    |  | |           | |  |
  |  | |    EC2    | |  |     |  | |    EC2    | |  |    |  | |    EC2    | |  |
  |  | |           | |  |     |  | |           | |  |    |  | |           | |  |
  |  | '-----------' |  |     |  | '-----------' |  |    |  | '-----------' |  |
  |  |               |  |     |  |               |  |    |  |               |  |
  |  |   Hardware 2  |  |     |  |   Hardware 4  |  |    |  |   Hardware 6  |  |
  |  '---------------'  |     |  '---------------'  |    |  '---------------'  |
  |                     |     |                     |    |                     |
  '---------------------'     '---------------------'    '---------------------'

```

- Pros:
  ..- Can span across Availability Zones (AZ)
  ..- Reduced risk in simultaneous failure
  ..- EC2 Instances are on different physical hardware
- Cons:
  ..- Limited to 7 instances per AZ per placement group
- Use Case:
  ..- Application that needs to maximize high availability
  ..- Critical Applications where each istance must be isolated from failure from each other

#### Partition

```
  .-----------------------------------------.     .-------------------.
  |               us-east-1a                |     |     us-east-1b    |
  |   .-------------.    .-------------.    |     |  .-------------.  |
  |   | .---------. |    | .---------. |    |     |  | .---------. |  |
  |   | |         | |    | |         | |    |     |  | |         | |  |
  |   | |   EC2   | |    | |   EC2   | |    |     |  | |   EC2   | |  |
  |   | |         | |    | |         | |    |     |  | |         | |  |
  |   | '---------' |    | '---------' |    |     |  | '---------' |  |
  |   | .---------. |    | .---------. |    |     |  | .---------. |  |
  |   | |         | |    | |         | |    |     |  | |         | |  |
  |   | |   EC2   | |    | |   EC2   | |    |     |  | |   EC2   | |  |
  |   | |         | |    | |         | |    |     |  | |         | |  |
  |   | '---------' |    | '---------' |    |     |  | '---------' |  |
  |   | .---------. |    | .---------. |    |     |  | .---------. |  |
  |   | |         | |    | |         | |    |     |  | |         | |  |
  |   | |   EC2   | |    | |   EC2   | |    |     |  | |   EC2   | |  |
  |   | |         | |    | |         | |    |     |  | |         | |  |
  |   | '---------' |    | '---------' |    |     |  | '---------' |  |
  |   | .---------. |    | .---------. |    |     |  | .---------. |  |
  |   | |         | |    | |         | |    |     |  | |         | |  |
  |   | |   EC2   | |    | |   EC2   | |    |     |  | |   EC2   | |  |
  |   | |         | |    | |         | |    |     |  | |         | |  |
  |   | '---------' |    | '---------' |    |     |  | '---------' |  |
  |   |             |    |             |    |     |  |             |  |
  |   | Partition 3 |    | Partition 3 |    |     |  | Partition 3 |  |
  |   '-------------'    '-------------'    |     |  '-------------'  |
  '-----------------------------------------'     '-------------------'

```

- Up to 7 partitions per AZ
- Can span across multiple AZs in the same region
- Up to 100s of EC2 instances
- The instances in a partition do not share racks with the instances in the other partitions
- A partition failure can affect many EC2 but won't affect other partitions
- EC2 instances get access to the partition information as metadata
- Use cases: HDFS, HBase, Cassandra, Kafka

### Elastic Network Interfaces (ENI)

- Logical component in a VPC that represents a **virtual network card**
- The ENI can have the following attributes:
  ..- Primary private Ipv4, one or more secondary IPv4
  ..- One Elastic Ip (IPv4) per private Ipv4
  ..- One Public IPv4
  ..- One or more security groups
  ..- A MAC Address

- You can create ENI independently and attach them on the fly (move them) on EC2 instances for failover
- Boudn to a specific availability zone (AZ)

#### EC2 Hibernate

- W eknow we can stop, terminate instances
  ..- Stop -- the data on disk (EBS) is kept intact in the next start
  ..- Terminate -- any EBS volumes (root) also set-up to be destroyed is lost

- On start, the following happens:
  ..- First start: The OS boots & The EC2 User Data script is run
  ..- Following starts: The OS boots up
  ..- Then your application starts, caches get warmed up, and that can take time

- When **Hibernate**
  ..- The in-memory (RAM) state is preserved
  ..- The instance boot is much faster! ( The OS is not stopped/restarted)
  ..- Under the hood: The RAM state is written to a file in the rot EBS volume
  ..- The root EBS volume must be encrypted

- Use cases:
  ..- Long-running processing
  ..- Saving the RAM state
  ..- Services that take time to initialize

Good to know

- Supported Instance Families -- C3, C4, C5, i3, m3, m4, r3, r4, t2, t3, ...
- Instance RAM size -- must be less than 150 GB.
- Instance Size -- not supported for bare metal instances
- AMI - Amazon Linux 2, Linux AMI, Ubuntu, ...
- Root Volume -- must be EBS, encrypted, not instance store, and large
- Available for On-Demand, Reserved and Spot instances

- An instance can NOT be hibernated more than 60 days

### EC2 Nitro

- Underlying Platform for the next generation of EC2 instances
- New virtualization technology
- Allows for better performance:
  ..- Better networking options (enhanced networking, HPC, IPv6)
  ..- Higher Speed EBS (Nitro is necessary for 64,000 EBS IOPS -- max 32,000 on non-Nitro)
- Better underlying security
- Instance types example:
  ..- Virtualized: A1, C5, C5a, C5ad, C5d, C5n, C6g, C6gd, D3,D3en, G4,I3en, infI, M5, M5a,M5d, M5dn,M5n,...
  ..- Bare metail: a1.metal, c5.metal, c5d.metal, c5n.metal, c6.metal, c6gd,metal...

### Understanding vCPU

- Multiple threads can run on one CPU (multihreading)
- Each thread is represented as a virtual CPU (vCPU)
- Example: m5.2xlarge
  ..- 4 CPU
  ..- 2 threads per CPU
  ..- => 8 vCPU in total

### Optimizing CPU options

- Ec2 instances come with a acombination of RAM and vCPU
- But in some cases, you may want to chagne the vCPU options:
  ..- # of CPU cores: you can decrease it (helpful if you need high RAM and low number of CPU) -- to decrease licensing costs
  ..- # of threads per core: Disable multithreading to hvae 1 thread per CPu -- helpful for high performance computing (HPC) workloads
- Only specified during instance launch

### Capacity Reservations

- Capacity Reservatoins ensure you have EC2 Capacity when needed
- Manual or palnned end-date for the reservation
- No need for 1 or 3 years commitment
- Capacity access is immediate, you get billed as soon as it starts
- Specify:
  ..- The Availbility Zone in which to reserve the capacity (only one)
  ..- The number of instnaces for which to reserve capacity
  ..- The instance attributes, inclding the instance type, tenancy and platform/OS
- Combine with Reserved Instances and Savings Plans to do cost saving

### EBS Volume

- An EBS (Elastic BLock Store) Volume is a netowrk drive you can attach to your istnaces while they run
- It allows your instances to persist data, even after theri termination
- They can only be mounted to one instance at a time ( at the CCP level )
- They bound to a specific availability zone

- Analogy: Think of them as a "network USB stick"
- Free Tier: 30GB of free EBS storage of type General Purpose (SSD) or Magnetic per month

- It's a network drive (i.e. Not a pysical drive)
  ..- It uses the network to communicate the instance, which means there might be a bit of latency
  ..- It can be detached from an EC2 instance and attached to another one quickly

- It's locked to an Availability Zone (AZ)
  ..- An EBS Volume in us-east-1a cannot be attached to us-east-1b
  ..- To move a volume across, you first need to snapshot it

- Have a provisioned capacity (size in GBs, and IOPS)
  ..- You get billed for all the provisoned capacity
  ..- You can increase the capacity of th drive over time

- Controls the EBS behavior when an EC2 instance terminates
  ..- By default, the root EBS volume is deleted (attribute enabled)
  ..- By default, any other attached EBS volume is not deleted (attribute disabled)
- This can be controlled by the AWS console / AWS CLI
- Use Case: Preserve root volume when instnace is terminated

### EBS Snapshots

- Make a backup (snapshot) of your EBS volume at a point in time
- Not necessary to detach volume to do snapshot, but remcommended
- Can copy snapshots across AZ or Region

- EBS snapshot Archive
  ..- Move a snapshot to an "archive tier" that is 75% cheaper
  ..- Takes within 24 to 72 hours for restroing the archive

- Recycle Bin for EBS Snapshots
  ..- Setup rules to retain deleted snapshots, so you can recover them after an accidental deleteion
  ..- Specify retention (from 1 day to 1 year)

### AMI (Amazon Machine Image)

- AMI are a customization of an EC2 instance
  ..- You add your own software, configuration, operating system, monitoring...
  ..- Faster boot/configuration time because all your software is pre-packaged
- AMI are build for a specific region (and can be copied across regions)
- You can launch EC2 instances from:
  ..- A public AMI: AWS provided
  ..- Your own AMI: you make and maintian them yourself
  ..- An AWS Marketplace AMI: an AMI someone else made (and potentially sells)

#### AMI process (from an EC2 instance)
```
.---------------.                                              .---------------.
|  us-east-1a   |                                              |  us-east-1b   |
|               |                .------------.                |               |
|  .----------. |                | Custom AMI |  Launch        |  .----------. |
|  | instance |----Create AMI--->|            |--from AMI----->|  | instance | |
|  '----------' |                '------------'                |  '----------' |
|               |                                              |               |
'---------------'                                              '---------------'
```
- Start an EC2 instance and customize it
- Stop the instance (for data integrity)
- Build an AMI -- this will also create EBS snapshots
- Launch instances from other AMIs

### Local EC2 Instance Store
- Need better performance than EBS ? 
- EBS volumes are network drives with good but "limited" performance
- If you need a high-erpformance hardware disk, use EC2 Instance Store

- Better I/O performance
- EC2 Instance Store lose theri storage if they're stopped (ephemeral)
- Good for buffer / cache /scratch data/ temporary content
- Risk of data loss if hardware fails
- Backups and Replication are your responsibility

### EBS Volume Type
- EBS volumes come in 6 types
..- gp2/gp3 (SSD): General purpose SSD volume that balances price and performance for a wide variety of workloads
..- io1/io2 (SSD): Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads
..- st1 (HDD): Low cost HDD volume designed for frequently accessed, throughput-intensive workloads
..- sc1 (HDD): Lowest cost HDD volume designed for less frequently accessed workloads
- EBS Volumes are charaterized in Size | Throughput | IOPS (I/O Ops Per Sec)
- Only gp2/gp3 and io1/io2 can be used as boot volumes

