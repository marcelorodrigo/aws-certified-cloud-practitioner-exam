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

## IAM
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

## Resources
- [Oficial Exam Guide](https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Exam-Guide.pdf)
- [6 advantages of Cloud Computing](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)
- [Types of Cloud Computing](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/types-of-cloud-computing.html)
- [ExamPro Course](https://www.youtube.com/watch?v=3hLmDS179YE)
- [AWS Well Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/wellarchitected-framework.pdf)
