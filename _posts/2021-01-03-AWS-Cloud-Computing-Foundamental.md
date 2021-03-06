---
layout:     post
title:      AWS Cloud Computing Foundamental
subtitle:   AWS Identity and Access Management(IAM), Elastic Compute Cloud(EC2), S3, VPC, NAT Gateway, NAT Internet
date:       2021-01-23
author:     Shuo Wang
header-img: img/post-bg-awslogo.jpg
catalog: true
tags:
    - AWS
    - Cloud Computing
    - IAM
    - EC2
---

![certificate](/img/AWS/CertificateStructure.png)

# Day1 What is AWS Identity and Access Management(IAM)

--

**AWS Identity and Access Management(IAM)** is a web service that enables Amazon Web Services(AWS) customers to manage users and user permissions in AWS. With IAM, you can centrally manage **users, security, credentials** such as access keys and **permissions** that control which AWS resources users can access.

**Manage IAM Users and their access:**
You can create Users and assign them individual security credentials (access keys, passwords, and multi-factor authentication devices). You can manage permissions to control which operations a User can perform.

**Manage IAM Roles and their permissions:**
An IAM Role is similar to a User, in that it is an AWS identity with permission policies that determine what the identity can and cannot do in AWS. However, instead of being uniquely associated with one person, a Role is intended to be assumable by anyone who needs it.

**Manage federated users and their permissions:**
You can enable identity federation to allow existing users in your enterprise to access the AWS Management Console, to call AWS APIs and to access resources, without the need to create an IAM User for each identity.

---

## My learned
Availability Zones (AZs): physical data center;  
Regions: server location in different cities; (one region has many AZs)  
Edge Locations: for higher density users, which loads the high frequency stuff into memory to make a lower latency, fast response and decrease system burden.  
Regional Edge Caches: for lower access things but in different regions, which provides a higher and faster access.  
one AZ has many Data Center  
one Region has many AZ(Availability Zone) (at least 2)  
each AZ is isolated with each other but closer with each other combined with lower latency.  
AWS AMI:  
Users: personal accessibility  
group: many users have same permissions  
Roles: **the service in AWS** communicate with other services in AWS (defines what you can do after you authenticate)e.g. EC2, S3  
policies: the permission of document for the templates for specific access rights; How many resources can be accessed.  
one Role has many policies.  
Profile: defines who you are for authentication  
[Introduction to AWS Identity and Access Management (IAM)](https://www.qwiklabs.com/focuses/15717?parent=catalog)

# Day2 What is Elastic Cloud Computing(EC2)?
A virtualized and abstracted subset of a physical server. It'll have access to storage, memroy and a network surface.  
After you configure your instance's operating system, the OS is defined by the Amazon Machine Image(AMI) you choose, and the hardware follows the instance type.  
Amazon Quick Start AMIs: include various releases of Linux or Windows Server OSs and some specialty images for performing common operations.  
AWS Marketplace AMIs: from the AWS Marketplace are official, production-ready images provided and supported by industry vendors like SAP and Cisco.  
Community AMIs: these images are AMIs created and maintained by independent vendors and are usually built to meet a specific need. This is a good catalog to search if you're palnning an application built on a custom combination of software resources.

## Instance Types
Instance Type Family:  
Accelerated computing: P3, P2, G3, F1 (machine learning, Neural network)  
based on cost for the instance types:  
**On-Demand Instances:** when you use, you cost; before have a higher volumn to use it. e.g. Black Friday. (按需)  
**Reserved Instances:** a contract that server one year(maybe). it becomes cheaper with longer development. (预留)  
**Spot Instances:** during peak computing level, it needs more money. (竞价)  
**Scheduled Reserved Instances:** periodically use server. (计划的预留)  
**Dedicated Instances & Dedicated Hosts:** VIP~!(专用) 



# Day3 What Is S3(Amazon Simple Storage Service)?
1. Maintaining backup archives, log files, and disaster recovery images  
2. Running analytics on big data at rest  
3. Hosting static websites  
It is an object storage. For EC2, it is a block storage which divided data into individual blocks whose use is managd by a file system. eg. NTFS exFAT. Allocating space for the files and data that are saved to the underlying device and for providing access whenever the OS needs to read some data.  
S3 standard --> S3 IA --> S3 Glacier [Amazon S3 Storage Classes](https://aws.amazon.com/s3/storage-classes/)  
Amazon Resource Names(ARN)s uniquely identify AWS resources across all of AWZ. eg. arn:aws:iam::414066325645:role/EC2InstanceProfileRole.  
AWS Policy generator: AWS policies use the JSON format, and are used to configure granular permissions for AWS services. Principal: EC2 Role ARN; Amazon Resource Name(ARN): the Bucket ARN that you previously copied(/*: restriction for all files ).  
[Introduction to Amazon Simple Storage Service S3](https://www.qwiklabs.com/focuses/15683?parent=catalog)

# Day4 What Is Virtual Private Clouds (VPCs)?
VPCs are easy-to-use AWS network organizers and great tools for organizing your infrastructure, which can be easy to isolate the instances in one VPC from whatever else you have running. eg. one VPC for application development, another for beta testing and a third for production.  
EC2 is located in the VPCs.  
VPC can logically isolated section of the Amazon Web Services(AWS) Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of **Your own IP address range**, **creation of subnets**, and **configuration of route tables** and **network gateways**
[Build a customer VPC](https://cidr.xyz/)

## Virtual Private Network(VPC)
Amazon’s Virtual Private Cloud service provides the networking layer of EC2. A VPC can exist only within an AWS region. A VPC is a virtual network that
can contain EC2 instances as well as network resources for other AWS services. By default, every VPC is isolated from all other networks.  
A VPC can exist only within an AWS region. When you create a VPC in a region, it won’t show up in any other regions. You can have multiple VPCs in your account and create multiple VPCs in a single region. To keep things simple, I’ll start by assuming only one VPC in one region. Later, I’ll cover considerations for multiple VPCs.
## VPC CIDR(Classless Inter-Domain Routing) Blocks
a VPC consists of at least one range of contiguous IP addresses. This address range is represented as a Classless interdomain routing (CIDR) block. You must assign a primary CIDR block when creating a VPC. For example, the CIDR 172.16.0.0/16 includes all addresses from 172.16.0.0 to 172.16.255.255—a total of 65,536 addresses!
## Secondary CIDR Blocks
You may optionally specify secondary CIDR blocks for a VPC after you’ve created it. These blocks must come from either the same address range as the primary or a publicly routable range, but they must not overlap with the primary or other secondary blocks. For example, if the VPC’s primary CIDR is 172.16.0.0/16, you may specify a secondary CIDR of 172.17.0.0/16. But you may not specify 192.168.0.0/16.
## Subnet and Elastic Network Interface
A subnet is a logical container within a VPC that holds your EC2 instances. A subnet lets you isolate instances from each other, control how traffic flows to and from your instances, and lets you organize them by function. For example, you can create one subnet for public web servers that need to be accessible from the Internet and create another subnet for database servers that only the web instances can access. In concept, subnets are similar to virtual LANs (VLANs) in a traditional network.  
Every instance must exist within a subnet. You’ll often hear the phrase “launch an instance into a subnet.” Once you create an instance in a subnet, you can’t move it. You can, however, terminate it and create a different instance in another subnet. By extension, this also means you can’t move an instance from one VPC to another.  
AWS reserves the first four and last IP addresses in every subnet. You can’t assign these addresses to any instances. Assuming a subnet CIDR of 172.16.100.0/24, the following addresses would be reserved:  
• 172.16.100.0–172.16.100.3  
• 172.16.100.255  
A subnet can exist within only one availability zone (AZ, or zone for short), which is roughly analogous to a relatively small geographic location such as a data center.

## NAT(Network Address Translation) Gateways
Network Address Translation (NAT) gateway to enable instances in a **private subnet** to connect to the internet or other AWS services, but prevent the internet from initiating a connection with those instances.  
step1 It must specify the public subnet in which the NAT gateway should reside. For more information about public and private subnets, see Subnet routing.  
step2 It must also specify an Elastic IP address to associate with the NAT gateway when you create it. The Elastic IP address cannot be changed after you associate it with the NAT Gateway.  
step3 After you've created a NAT gateway, you must update the route table associated with one or more of your **private subnets** to point internet-bound traffic to the NAT gateway. This enables instances in your private subnets to communicate with the internet. [Details](https://blog.csdn.net/Ahri_J/article/details/105348678#:~:text=NAT%20Gateway%EF%BC%88%E7%BD%91%E7%BB%9C%E5%9C%B0%E5%9D%80%E8%BD%AC%E6%8D%A2,%E8%AE%BF%E9%97%AE%EF%BC%8C%E6%8F%90%E9%AB%98%E4%BA%86%E5%AE%89%E5%85%A8%E6%80%A7)
![picture11](/img/AWS/NATgateway.png)

## NAT Instance
NAT Instance: package forwarding. Compared with NAT Gateway, it is more flexible to do load balancer, not convenient.


## Internal IP range
10.0.0.0 - 10.255.255.255(10/8 prefix)  
172.16.0.0 - 172.31.255.255 (172.16/12 prefix)  
192.168.0.0 - 192.168.255.255 (192.168/16 prefix)

## VPC Peering
Allow one VPC connect with another one via a direct network route using private IP addresses.  
It can be in the same AWS account or other account.  
Peering is a star configuration. No transitive peering!

## Network Access Control Lists (Network ACL)
A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. You might set up network ACLs with rules similar to your security groups in order to add an additional layer of security to your VPC. [Details](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html)  
#### Remember points:
1. Network ACLs have **separate** inbound and outbound rules, and each rule can either **allow or deny** traffic.  
2. The VPC automatically comes **a default network ACL** and by default it allows all **outbound** and **inbound** traffic.  
3. For creating custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.  
4. Each subnet in the VPC **must be** associated with network ACL. If you do not explicity associate a subnet with a network ACL, the subnet is **automatically associated with the default network ACL**.  
5. A network ACL can apply in multiple subnets; However, a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.  
6. The lower rule number has the higher priority.  
7. Network ACLs are stateless; responses to allowed inbound traffic are subject to the rules for outbound traffic.

# Day5 CloudTrail and Events
CloudTrail logs both API and non-API actions. Non-API actions include logging into the management console. API actions include launching an instance, creating a bucket in S3, and creating a virtual private cloud (VPC).
These are API events regardless of whether they’re performed in the AWS management console, with the AWS
Command Line Interface, with an AWS SDK, or by another AWS service. CloudTrail classifies events into management events and data events.

### Management Events
Management events include operations that a principal executes (or attempts to execute) against an AWS
resource. AWS also calls management events control plane operations.

Management events are further grouped into write-only and read-only events. Writeonly events include API
operations that modify or might modify resources. For example, the RunInstances API operation may create a
new EC2 instance and would be logged, regardless of whether the call was successful. Write-only events also
include logging into the management console as the root or an IAM user. CloudTrail does not log unsuccessful
root logins. Read-only events include API operations that read resources but can’t make changes, such as the
DescribeInstances API operation that returns a list of EC2 instances.
### Data Events
Data events track two types of data plane operations that tend to be high volume: S3 object-level activity and
Lambda function executions. For S3 object-level operations, CloudTrail distinguishes read-only and writeonly
events. GetObject is a read-only event, while DeleteObject and PutObject are write-only events.

### Event History
By default, CloudTrail logs 90 days of management events and stores them in a viewable, searchable, and
downloadable database called the event history. The event history does not include data events.
CloudTrail creates a separate event history for each region containing only the activities that occurred in that
region. But events for global services such as IAM and Route 53 are included in the event history of every
region.

## Cloud Watch Metrics
CloudWatch functions as a metric repository that lets you collect, retrieve, and graph numeric performance metrics
from AWS and non-AWS resources. All AWS resources automatically send their metrics to CloudWatch. These
metrics include EC2 instance CPU utilization, EBS volume read and write IOPS, S3 bucket sizes, and DynamoDB
consumed read and write capacity units. Optionally, you can send custom metrics to CloudWatch from your
applications and on-premises servers. CloudWatch Alarms can send you a notification or take an action based on the
value of those metrics. CloudWatch Logs lets you collect, store, view, and search logs from AWS and non-AWS
sources. You can also extract custom metrics from logs, such as the number of errors logged by an application or the
number of bytes served by a web server.
![picture1](/img/AWS/CloudWatch.png)
# Day6 AWS Config
AWS Config tracks how your AWS resources are configured at a point in time. Resources are entities that you
create and manage using the management console, AWS CLI, or AWS SDKs. Think of AWS Config as a time
machine. You can use it to see what a resource configuration looked like at some point in the past versus what it
looks like now.

CloudTrail logs events, and CloudWatch can alert on events, but only AWS Config gives you a holistic view of
your resources and how they were configured at any point in time. AWS Config can help you with the following
objectives:

• Security AWS Config can notify you whenever a resource configuration changes, alerting you to potential
breaches. You can also see what users had which permissions at a given time.

• Easy Audit Reports You can provide a configuration snapshot report from any point in time.

• Troubleshooting You can analyze configurations around the time a problem started. AWS Config makes it easy
to spot misconfigurations and how a problem in one resource might impact another.

• Change Management AWS Config lets you see how a potential change to one resource could impact another.
For example, if you plan to change a security group, you can use AWS Config to quickly see all instances that
use it.

## Domain Name System (DNS)
making your resources available across a
network using a human-readable name.
![picture2](/img/AWS/DNSprocess.png)

A domain name is made up of multiple parts. The rightmost text of every domain address (like .com or .org)
indicates the top-level domain (TLD). The name to the left of the TLD (the amazon part of amazon.com) is
called the second-level domain (SLD). This SLD designation would also refer to the unique second-level
domains used by some countries, like the .co of .co.uk that’s used for UK-based businesses.
A subdomain identifies a subset of a domain’s resources.
![picture4](/img/AWS/domain.png)

## Route 53
Amazon’s Route 53 is built to manage domain services, but it can also have a significant impact on the
precision and speed with which resources are delivered.
Route 53 provides morex
than just basic DNS services. In fact, it focuses on four distinct areas: domain registration, DNS management,
availability monitoring (health checks), and routing policies (traffic management).
![picture5](/img/AWS/healthcheck.png)

## CloudFront
Is is a content delivery web service. It integrates with other AWS products to give developers and businesses an easy way to distribute content to end users with low latency, high data transfer speeds, and no minimum usage commitments. Amazon’s global content delivery network (CDN), can take both speed and accuracy a few steps further. 
![picture6](/img/AWS/CloudFront.png)
![picture7](/img/AWS/CloudFront2.png)


# Day7 AWS Lambda
It is a compute service that runs your code in response to events and automatically manages the compute resources for you. eg. image upload, in-app activity, website click, or output from a connected device.
[quick lab](https://www.qwiklabs.com/focuses/15682?parent=catalog)

# Day8 Database on AWS
RDS - back up, multi-AZ(for disaster recovery) & read replicas(for scaling and fast reading)  
DynamoDB (NoSQL)  
RedShift (OLAP: Online Analytical Processing, for analysis. OLTP: Online Transaction Processing, for data save)  
Elasticache: quickly access in the RAM for two memory caching engines: Memcached and Redis  
Aurora: for serverless RDBMS  

## AWS RDS (Relational Database)
RDBMS: SQL Server, Oracle, MySQL, PostgreSQL, Aurora, MariaDB  
Automated Backups: backup(in S3) in a sepcific time with transaction logs to restore a database. The automated backup will be deleted when the RDS instance is stopped.  
Snapshots: mannually backup, which can be keep after you delete the original RDS instance.
## What is ARN?
ARN: Amazon Resouce Name (unique identity), which will be used for encrypted database.

## The different between Multi-AZ Deployments with Read Replicas
![picture8](/img/db/database1.png)

## Comparison with SQL and NoSQL
Collection == Table  
Document == Row  
Key Value Pairs == Fields  

## RDS Structure
![picture8](/img/AWS/RDS2.jpg)
![picture9](/img/AWS/RDS1.png)
M: master; S: Slaver; R can be used as DB backups, which is asnchronous and can also be used in read workloads.

## DynamoDB
It is a fast and flexible NoSQL database, which is a fully managed database and supports both document and key-value data models, suitable for mobile, web, gaming, at-tech, IOT. Stored on SSD storage with spread across 3 geographically distinct data centers.  
Eventual Consistent Reads: fast read with little latency.
Strongly Consistent Reads: reflects all writes that received a successful response piror to the read.(higher consistency with lower performance).

## RedShift
Amazon Redshift is a fast and powerful, fully managed, petabyte-scale data warehouse service in the cloud.(OLAP)  
ATTENTION: OLAP & OLTP have no relationship with NoSQL.  
Redshift has Multi-Node including one master node(leader node: manges client connections and receives queries) and many compute noded/slaver worker(store data and perform queries and computations.)  
Firstly, RedShift is columnar data storage, which organizes the data by column. Column-based systems are ideal for data warehousing and analytics. Data is stored sequentially on the storage media, column-based sstems require far fewer I/Os, greatly improving query performance. Secondly, It has provide significant compression in the same data type in the columns, which means Amazon Redshift automatically samples your data and selects the most appropriate compression scheme. Thirdly, Massively Parallel Processing(MPP): automatically distributes data and query load across all ndes. easily to add nodes and maintian fast query performance.

## AWS Aurora
MySQL-compatible that combines the speed and availability of high-end commercial databases, which performance 5 times better than MySQL while delivering similar performance and availability.

## Elasticache
Elasticache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud, which allows you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.  
1. Memcached  
Elasticache is protocol compliant with Memcached, so popular tools that you use today with existing Memcached environments will work seamlessly with the service.  

2. Redis  
A popular open-source in-memory key-value store that supports data structures, such as sets and lists. Elasticache supports master/slave replication and multi-AZ which can be used to achieve cross AXZ redundancy.  
Aurora storage is self-healing. Data blocks and disks are continuously scanned for errors and repaired automatically.
