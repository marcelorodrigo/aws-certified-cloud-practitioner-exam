# AWS Certified Cloud Practitioner Exam
My topics and notes used when studying to AWS Certified Cloud Practitioner (CLF-C01) Examination

## Goal
The AWS Certified Cloud Practitioner (CLF-C01) examination is intended for individuals who have the knowledge,
skills, and abilities to demonstrate basic knowledge of the AWS platform, including:
- Available services and their common use cases
- AWS Cloud architectural principles (at the conceptual level)
- Account security and compliance.

In the result, you're able to demonstrate an understanding of AWS Cloud economics including: costs, billing, and analysis,
and the value proposition of the AWS Cloud.

## Six Advantages of Cloud Computing
**Trade capital expense for variable expense** – Instead of having to invest heavily in data centers and servers before you know how you’re going to use them, you can pay only when you consume computing resources, and pay only for how much you consume.

**Benefit from massive economies of scale** – By using cloud computing, you can achieve a lower variable cost than you can get on your own. Because usage from hundreds of thousands of customers is aggregated in the cloud, providers such as AWS can achieve higher economies of scale, which translates into lower pay as-you-go prices.

**Stop guessing capacity** – Eliminate guessing on your infrastructure capacity needs. When you make a capacity decision prior to deploying an application, you often end up either sitting on expensive idle resources or dealing with limited capacity. With cloud computing, these problems go away. You can access as much or as little capacity as you need, and scale up and down as required with only a few minutes’ notice.

**Increase speed and agility** – In a cloud computing environment, new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes. This results in a dramatic increase in agility for the organization, since the cost and time it takes to experiment and develop is significantly lower.

**Stop spending money running and maintaining data centers** – Focus on projects that differentiate your business, not the infrastructure. Cloud computing lets you focus on your own customers, rather than on the heavy lifting of racking, stacking, and powering servers.

**Go global in minutes** – Easily deploy your application in multiple regions around the world with just a few clicks. This means you can provide lower latency and a better experience for your customers at minimal cost.

## Types of Cloud Computing
**Infrastructure as a Service (IaaS)** - Contains the basic building blocks for cloud IT and typically provides access to networking features, computers (virtual or on dedicated hardware), and data storage space. IaaS provides you with the highest level of flexibility and management control over your IT resources and is most similar to existing IT resources that many IT departments and developers are familiar with today.

**Platform as a Service (PaaS)** - Removes the need for your organization to manage the underlying infrastructure (usually hardware and operating systems) and allows you to focus on the deployment and management of your applications. This helps you be more efficient as you don’t need to worry about resource procurement, capacity planning, software maintenance, patching, or any of the other undifferentiated heavy lifting involved in running your application.

**Software as a Service (SaaS)** - Provides you with a completed product that is run and managed by the service provider. In most cases, people referring to Software as a Service are referring to end-user applications. With a SaaS offering you do not have to think about how the service is maintained or how the underlying infrastructure is managed; you only need to think about how you will use that particular piece of software. A common example of a SaaS application is web-based email which you can use to send and receive email without having to manage feature additions to the email product or maintain the servers and operating systems that the email program is running on.

# Well Architected Framework
- Operational Excellence
  - Ability to run and monitor systems
  - Infra as code
  - Frequent, small and reversible changes
  - Antecipate failures
- Security
  - Ability to procted info, systems and assets
  - Least privilege principle (IAM)
  - Automated with best pratices
- Realiabilty
  - Ability to recover from infra or service disruptions
  - Scale horizontally to increase aggreate system availability
  - Stop guessing capacity with auto scale
- Performance Efficiency
  - Ability to use computing resources efficiently
  - Go global in minutes
  - Serverless architectures
- Cost Optimization
  - Ability to run systems to deliver business value at the lowest price point
  - Pay only for what you use
  - Use Cloudwatch
  - Tags to catalog resources

# IAM
- IAM is a Global service
- Root account should not be used to operate AWS, as it not follows the least previlege principle
- Users should be created instead, they can be grouped
- Groups can only contain users (not other groups)
- Users are not required to belong to a group, but they can belong of multiple groups
- Policies (JSON) can be applied to groups or users
- Roles for EC2 Instances or AWS Services
- IAM Credential Reports and IAM Access Advisor can help you audit IAM usage
- Some best practices for IAM are: To use MFA (Multi Factor Authentication), to use a good password policy for users, to never share IAM users or access keys!

# EC2
## Instances Purchase Options
- On-Demand
- Reserved
  - 1y minimum
  - Convertible: long jobs with flexible instances types over time
  - Scheduled: for a repeated time scheduled reservation
- Spot: short jobs and cheap. But you can easily lose it due to the pricing model.
- Dedicated
  - Dedicated Host: to have a physical server just for you.
  - Dedicated Instance: hardware is dedicated to you, you may share the hardware with other instances in your account and no control over which your dedicated hardware your instance will be running.

# EBS
- Volumes are network drives that can be mounted to an instance at time (consider as true to this exam context)
- Persists data that still lives even after instance termination
- Bound to a specific AZ
- Snapshots can be copied to any region
- AMI's are built to a specific region, but they can be copied across regions
- EC2 Image Builder automate the creation, maintaining, validation and testing of AMI's (and it can be scheduled)
- EC2 Local Instance Store can be used to speed up a physical disk connection to EC2 instance
- EFS is a NFS that can be mounted to several EC2 instances at once, and it costs 3x more than an EBS. It's multi AZ inside a region

# ELB
- High availability means your app running at least in 2 availability zones
- Scability: ability to accomodate a larger load by increasing the hardware (scaling up) or by adding nodes (scale out)
- Elasticity: after the system is being scalable, elasticity means that the system can auto-scale based on the load
- 4 kinds of load balancers:
  - Application Load Balancer (http[s] only)
  - Network Load Balancer
  - Gatewau Load Balancer
  - Classic Load Balancer (deprecated, old genereation)

# S3
- Naming conventions for buckets
  - No uppercase
  - No underscore
  - 3-63 characters long
  - No IP numbers
  - Must start with lowercase letter or number
  - It needs to be globally unique
- There isn't directory/folder concept, but prefixes that are part of the object key that can be long and with slashes (/)
- Max object size is 5TB (which needs to be uploaded with multipart if they are bigger than 5 GB)
## Security
Any access can be granted to an object if any of the conditions below are true, and there's no explict DENY.
### User Based
- IAM Policies: attaching IAM policies for a specific user
### Resource Based
- Bucket policies, where rules are attached directly to buckets
- Object Access Control List (OACL) - granular control
- Bucket Access Control List (BACL)
## Replication
- Versioning is required for replication
- Cross Region Replication [CRR]: compliance, lower latency, replicate between accounts
- Same Region Replication [SRR]: log aggregation, live replication between prod and test accounts
- Buckets can be in different accounts
- Asynchronous process
## Storage Classes
- Amazon S3 General Purpose Storage
- Amazon S3 Standard Infrequent Access (IA)
- Amazon S3 One Zone-Infrequent Access.
- Amazon S3 Intelligent Tiering
- Amazon S3 Glacier
- Amazon S3 Glacier Deep Archive

# Databases and Analytics
- Relational Databases (OLTP): RDS / Aurora
- Memory: ElastiCache
- Key-Value: DynamoDB (Serverless) + DAX (DynamoDB Accelerator Cache)
- Warehouse (OLAP): Redshift
- Hadoop Cluster: EMR
- Athena: query data from S3
- Quicksight: Dashboards from your data
- DocumentDB: Amazon Aurora for MongoDB
- QLDB: Financial Transactions Ledger
- Managed Blockchain
- Glue: Transform data using ETL for Redshift
- Database Migration: DMS
- Graph Database: Neptune

# System Manager (SSM)
- Helps you to manage EC2 and On-Premises system at scale, in a hybrid way.

# OpsWorks
- Chef & Puppet as a service, an alternative to SSM

# Monitoring
- CloudWatch
  - Metrics: monitor services performance and biling metrics
  - Alarms: automate notification, perform ec2 actions, notifications via SNS based on metrics
  - Logs: collect logs from EC2, servers, lambdas, etc
  - Event Bridge: react to events or trigger a rule based on a schedule
- CloudTrail: audit API calls within your account
- CloudTrail Insights: automated analysis of your CloudTrail events
- X-Ray: trace requests through your services

# Security
- Shared Responsability Model
  - Customer is responsible for security **IN** the cloud (customer data, platforms, applications, OS, network configuration and security, firewall, client and server side encryption, etc)
  - AWS is responsible for security **OF** the cloud (compute, storage, database, networking, hardware, local access security, power, regions, availability zones and edge locations)
- WAF & Shield for DDoS protection
- AWS KMS (Key Management Service) is responsible to manage encryption keys for AWS Services at a software level
- CloudHSM manage encryption at a hardware level (HSM = Hardware Security Module)
- AWS Secret Manager for secret management (mostly on the exam related to RDS)
- AWS Artifact: not really a service, but on demand compliance documentation and AWS agreements
- GuardDuty, Macie and Security Hub are used to identify possible security issues
- Detective is used for deep findings and analysys on the possible root cause on the issues identified by the services above
- Abuse to report for abusive or illegal purposes that you detect
- Actions that can be only performed by the root user
  - Change account settings
  - Close your account
  - Change or cancel support plans
  - Register as reseller on Reserved Instance Marketplace
  - Signup for GovCloud

# Accounts
- AWS Organizations to organize organizational units and SCP (service control policies) to restrict accounts powers
- AWS Control Tower to setup multi acccount environment according with best pratices
- Config to record all resources configurations and compliance over time
- CloudFormation to deploy stacks
- CloudTrail to record API calls made within your account

# Billing
- AWS Pricing Calculator can help you estimate costs for your solution
- AWS Biling Dashboard show your monthly costs in a high level overview
- Cost Allocation tracks costs on a detailed level
- Cost Explorer allows you to visualize, understand and manage your costs and usages over time
- Trusted Advisor analyse your accounts and provides recommendations on:
  - Cost Optimization
  - Performance
  - Security
  - Fault Tolerance
  - Service Limits
- Full Trusted Advisor available on Business and Enterprise plans

# Support
## Basic Support
- Customer Service and Communities
- AWS Trusted Advisor (core checks only)
- AWS Personal Health Dashboard
## Developer
- Business hours emails access to Cloud Support Associates
- Unlimited Cases / 1 primary contact
- SLA for response times
  - General Guidance: <=24 business hours
  - System impaired: <=12 business hours
## Business
- Full Trusted Advidor + API access
- 24x7 phone email and chat to Cloud Support Engineers
- Unlimited cases / Unlimited contacts
- Access to Infrastructure Event Management for an additional fee
- SLA for response times
  - General Guidance: <=24 business hours
  - System impaired: <=12 business hours
  - Production System Impaired: <=4 hours
  - Production System Down: <=1 hour
## Enterprise
- Access to Technical Account Manager (TAM)
- Concierge Support Team (for billing and account best pratices)
- Infrastructure Event Management, Well-Architected & Operation Reviews
- SLA for response times
  - same as business
  - Business-critical system down: <=15 minutes

## Resources
- [Oficial Exam Guide](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf)
- [6 advantages of Cloud Computing](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)
- [Types of Cloud Computing](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/types-of-cloud-computing.html)
- [ExamPro Course](https://www.youtube.com/watch?v=3hLmDS179YE)
- [AWS Well Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/wellarchitected-framework.pdf)
