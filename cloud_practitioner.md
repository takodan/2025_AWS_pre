# AWS Certified Cloud Practitioner
## 0. Resources
- [Ultimate AWS Certified Cloud Practitioner CLF-C02 2025](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/)
## 1. Cloud and Cloud Computing
1. Cloud provider owns and maintains the hardware, while you provision exactly the type and size you need via a web application.

2. Types of Cloud 
    1. Private Cloud: e.g. rackspace
    2. Public Cloud: e.g. MS Azure, GCP, AWS
    3. Hybrid Cloud

3. Five Characteristics of Cloud
    1. On-demand self service
    2. Broad network access
    3. Multi-tenancy and resource pooling
        - multiple customers can share the same infrastructure
    4. Rapid elasticity彈性 and scalability 
    5. Measured service:
        - Pay-as-you-go pricing

4. Six Advantages
    1. Trade capital expense (CAPEX) for operational expense (OPEX)
        - reduced Total Cost of Ownership (TCO)& Operational Expense (OPEX)
    2. Benefit from massive economies of scale
    3. stop guessing capacity
    4. increase speed and agility
    5. Stop spending money running and maintaining data centers
    6. Go global in minutes

5. Problems solved
    1. Flexibility
    2. Cost-Effectiveness
    3. Scalability
    4. Elasticity
    5. Hight-availability abd fault-tolerance
    6. Agility

6. Types of Cloud Computing
    1. Infrastructure as a Service
        - Provides hardware for customer
        - AWS EC2
    2. Platform as a Service
        - Underlying infrastructure managed by service provider
        - Elastic Beanstalk on AWS
    3. Software as a Service
        - Product is run and managed by the service provider
        - Rekognition for Machine Learning on AWS
        - Gmail, Dropbox, Zoom
    
7. AWS Pricing Overview
    1. Pay-as-you-go
    2. Compute: pay for compute time
    3. Storage: pay for data stored in the cloud
    4. Data transfer: out of the cloud, in is free

8. AWS Infrastructure
    1. AWS Regions
        - a cluster of data center
        - Most AWS services are region-scoped
    2. AWS Availability Zone
        - Each region has many availability zones (min 3, max 6)
        - Each AZ is one or more discrete data center with redundant power, networking, ect.
        - isolated from disasters
    3. AWS Edge Location/ Point of Presence
        - for delivered content to end user with lower latency

9. How to choose an AWS Region
    1. Compliance遵守 with data governance and legal requirements
    2. Latency
    3. Available services with in a Region
    4. Pricing

10. Shared Responsibility Model
    1. Customer: Responsibility for the security **IN** the cloud
    2. AWS:Responsibility for the security **OF** the cloud



## 2. Identity and Access Management (IAM)
1. IAM
    1. Root account: shouldn't be used or shared 
    2. Users: can be grouped and be in multiple groups but you don't have to 
    3. User Groups: only contain users, not other groups
    4. Roles: Permissions for AWS services instead of Users

2. Permissions
    1. Assign JSON documents (policies) to User or Groups
    2. Least privilege principle: don't give more permissions then a user needs
    3. AWS has a lot of standard permission policies ready to go

3. IAM Policies Structure
```JSON
{
    "Version": "2012-10-17", // policy language version
    "Id": "S3-Account-Permissions", //policy id (optional) 
    "Statement": [
        {
            "Sid": "1", // statement id (optional)
            "Effect": "Allow", // Allow, Deny
            "Principal": { // this policy applied to
                "AWS": ["arn:aws:iam::123456789012:root"]
            },
            // list of action this policy allows or denies
            "Action": [
                "s3:GetObject",
                "s3:PutObject"
            ], // * for everything
            // list of resources to  witch the action applied to
            "Resources": ["arn:aws:s3:::mybucket/*"] 
            // * for everything
            // "Condition" conditions for when this policy is in effect (optional)
        }
    ]

}
```

4. IAM Password policy
    1. password length, specific character, etc.
    2. MFA (multi factor authentication)

5. Access AWS
    1. Management Console: password + MFA
    2. Command Line Interface (CLI): access key
        - Users manage their own access key
            ```bash
            aws configure
            # enter Access Key ID
            # enter Secret Access Key
            # enter default region name
            # enter default output format (optional)
            ```

        - You can also use CloudShell in Management Console
            - You don't need to enter access key in CloudShell
            - You can create, upload, and download files in CloudShell
    3. Software Developer Kit (SDK): access key

6. IAM Security tools
    1. IAM Credentials Report (account level)
        - lists all your account's users and their status
    2. IAM Last Accessed (user level)
        - shows the service permissions granted and have been used by a user
    3. IAM Access Analyzer

7. IAM Best Practices
    1. Don't use the root account except for account setup
    2. One physical user = One AWS user
    3. Assign users to groups
    4. Use strong password policy and MFA
    5. Create Roles for giving permission to AWS services
    6. Use Credentials Report and Last Accessed

8. Shared Responsibility Model for IAM
    1. YOU:
        1. Users, Roles, Policies management and monitoring
        2. Enable MFA
        3. Rotate all your keys often
        4. Apply appropriate permission
        5. Analyze access patterns and review permissions
    2. AWS:
        1. Infrastructure

3. IAM workflow cheat sheet
    1. Users > Create user > Set permissions (Add user to a groups)
    2. Users need account ID or account alias to log in
    3. Users > choose a user to edit permissions/groups
    4. Policies > Create policy > Visual/JSON
    5. Account Settings > Edit password policy
    6. Users > choose a user > security credentials > Access key
    7. Roles > create role > AWS service
    8. Credentials report
    9. Users > choose a user > Last Accessed


## 3. Elastic Computer Cloud (EC2)
1. Budget setup
    1. Billing info is Root account access only
    2. Enable IAM users access
        1. Root account > Account (Top-right menu)
        2. IAM user and role access to Billing information
    3. Billing and Cost Management (Top-right menu) > Budgets

2. EC2
    1. It's Infrastructure as a service
    2. Renting virtual machines (EC2)
    3. Storing data on virtual drives (EBS)
    4. Distributing load across machines (ELB)
    5. Scaling the services using an auto-scaling group (ASG)

3. EC2 configuration option
    1. OS
    2. RAM
    3. CPU
    4. Storage
        1. Network-attaches (EBS and EFS)
        2. Hardware (EC2 instance Store)
    5. Network card
    6. Firewall rules
    7. Bootstrap script (EC2 User Data): Script that only run once at the first start

4. Hands-On: launching an EC2 Instance
    1. Launching a instance using the AWS Console
        1. `EC2` > `Instances` > `Launch instances`
        2. Name, Images, Instance type
        3. Key pair: for connect to the instance
        4. Network settings > Firewall > Allow SSH, HTTP
        5. Configure storage > Advance > Delete on termination
        6. Advanced details > User data
        7. Launch instance
    2. Access instance via public IPv4 address
        1. when reboot a instance, public IPv4 may change

5. [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
    1. Naming convention
        1. `m5.2xlarge`
        2. `m`: instance class
        3. `5`: generation
        4. `2xlarge`: size within the instance class (CPU, RAM, etc.)
    2. 

6. EC2 Security Groups
    1. Acting as a firewall on EC2 instances
    2. Security Groups only contain **allow** rules
    3. Security Groups regulate
        1. Access to Ports
        2. Authorized IP ranges
        3. Control of inbound network
        4. Control of outbound network
    4. It locked down to a region/VPC combination
    5. It's good to maintain one separate Security Group for SSH access
    6. By default
        1. All inbound is blocked
        2. All outbound is authorized
    7. Referencing other Security Groups in a Security Group
        1. This allow other instances to access the instance
        2. If
            1. Security Group 1 inbound authorizing Security Group 2
            2. Instances with Security Group 2 can send request to all instances with Security Group 1

7. Hands-On: EC2 Security Groups
    1. `EC2` > `Security Groups` > select a Security Group
    2. 0.0.0.0/0 mean any IP is allow

8. Classic Ports
    1. 22 SSH: log into a Linux instance
    2. 21 FTP: upload file to a file share
    3. 22 SFTP: upload file using SSH
    4. 80 HTTP
    5. 443 HTTPS
    6. 3389 RDP: log into a Windows instance

10. connect to an EC2 instance via SSH
    1. default instance user name: `ec2-user`
    2. Linux/Mac
    ```bash
    chmod 0400 [YourSSHKey].pem # change .pem file permission
    ssh -i [YourSSHKey].pem ec2-user@[InstancePublicIP]
    exit
    ```
    3. Windows
        1. PuTTY
            1. need .ppk file to work
            2. use PuTTYgen to generate .ppk file from .pem file
            3. PuTTY > enter Host Name `ec2-user@[InstancePublicIP]`
            4. Save as New Session
            5. Connection > SSH > Auth > Private key file...
            6. open .ppk file 
            7. Save the Session just create
            8. Open Session

        2. Windows 10 and up have ssh command
            1. change .pem file permission in file Properties
                1. Security > Advanced > Disable inheritance
                2. Add > Select a principal
                3. Full control
            2. Cmd or PowerShell
            ```bat
            ssh -i ./[YourSSHKey].pem ec2-user@[InstancePublicIP]
            exit
            ```
    4. EC2 instance connect
        1. AWS EC2 page > select an instance > Connect

11. EC2 IAM Role
    1. AWS `EC2` page > select an instance > `Actions` > `Security` > `Modify IAM role`
    2. then the instance can use `aws` command to access the AWS

12. EC2 Purchasing Options
    1. On-Demand Instance
        1. Linux or windows: billing per second
        2. other OS: billing per hour
        3. for short-term and un-interrupted workload
    2. Reserved (1 and 3 years)
        1. Reserved Instances
            1. up to around 70% discount compared to On-demand
            2. reserve a specific instance attribute, period, region or zone
            3. Pay: No upfront, Partial upfront, all Upfront
            4. for steady-state usage
            5. can trade in the Reserved Instances Marketplace
        2. Convertible Reserved Instances: 
            1. around 70% discount compared to On-demand
            2. more flexible: can change instance type, OS, etc.
    3. Saving Plans (1 and 3 years): 
        1. discount same as Reserved Instances
        2. commitment to an amount of usage (e.g. $10/hour for 3 years)
        3. locked to a specific instance family and region
    4. Spot Instance:
        1. for short workloads (distributed workloads, batch jobs)
        2. up to around 90% discount, less reliable
        3. if your max price is less then the current spot price, you can **lose** an instance
    5. Dedicated Hosts: 
        1. book an entire physical server, control instance placement
        2. for address compliance requirements and use a existing server-bound software licenses
        3. can be On-Demand or Reserved
        4. the most expensive option
    6. Dedicated Instance:
        1. instance run on hardware that's dedicated to you
        2. but no control over instance placement
    7. Capacity Reservations:
        1. reserve On-Demand capacity in a specific AZ fot any duration
        2. no time commitment and discounts (On-Demand price)
        3. charge whether you run instances or not
        4. for short-term workloads that need to be in a specific AZ

13. Shared Responsibility Model for IAM
    1. YOU:
        1. Security Groups rules
        2. OS patches and updates
        3. Software and utilities installed 
        4. IAM Roles assigned to EC2
        5. Data security
    2. AWS:
        1. Infrastructure

14. Elastic Block Store (EBS) Volume
    1. It's a net work drive you can attach to an instance
        - might have latency
        - can be detached then attached to another instance
    2. It's for an instance to persist data after they been terminated
    3. One EBS can only be mounted to one EC2 instance
        - One instance can have multiple EBS
        - Associate level certificate: some EBS have multi-attach feature
    4. It bound to a specific AZ (EC2 and EBS have to be in the same AZ)
        - You need to snapshot an EBS to move it across AZ
    5. Have a provisioned capacity (GBs and IOPS)
    6. When an instance , by default
        - root EBS volume will be deleted
        - any other EBS volume will not be deleted
        - controls the behavior by the `Delete on Termination` attribute
        - change a default attribute when launching an instance
    7. Hands-On: EBS
        1. `EC2` > `Instances` > select an instance > storage: to manage an instance's EBS
        2. `EC2` > `Volume`: to create, attach, snapshot an EBS
        3. Make sure the EC2 and the EBS are in the same AZ

15. EBS Snapshot (backup)
    1. Can be made at any time and copy across AZ or Regions
    2. Not necessary to detach volume to do snapshot, but recommended
    3. EBS Snapshot Archive
        1. move a snapshot to an archive tier
        2. It's cheaper but take 24 to 72 hours for restoring
    4. Recycle Bin for EBS Snapshot
        1. Setup rules to retain deleted snapshots
        2. retain 1 day to 1 year
    5. manage snapshot at `EC2` > `Snapshots`
        1. right click a snapshot > `Copy snapshot`: can copy to another AZ or Region
        2. `Action` > `Create Volume from snapshot`: also can create to another AZ or Region
    6. Recycle Bin is a stand-alone service in AWS

16. Amazon Machine Image (AMI)
    1. Using customized EC2 instance to create an  customized AMI
    2. Public AMI: AWS provided
    3. AWS Marketplace AMI: AMI made by someone else
    4. Hands-On: AMI
        1. `EC2` > right click an instance > `Image and templates` >`Create image`
    5. EC2 Image builder
        1. Automate the creation of VM or image
        2. workflow: EC2 Image builder > create Builder EC2 Instance > create AMI and teat EC2 instance
        3. Can be run on a schedule
        4. Free (only pay for the instance and AMI)

17. EC2 Instance Store
    1. Some instance types have Instance Store
    2. They have better I/O performance, but they are ephemeral storage (lose when it stop)
    3. Good for buffer/ cache/ scratch data/ temporary content
    4. Risk of data loss if hardware fails

18. Elastic File System (EFS)
    1. Managed NFS for EC2
    2. Can be attach to 100s of EC2
    3. Works with Linux EC2 in multi AZ
    4. Highly available, scalable
    5. Expensive, pay per use, no capacity planning
    6. When setup an EFS, you can choose `Transition into Infrequent Access (IA)` value
        1. Up to around 90% lower cost when store in IA
        2. e.g. 
            1. value = 60 days
            2. files haven't been use for 60 days will automatically move to IA

19. Amazon FSx
    1. FSx for Windows File Server
        1. Windows native shared file system
        2. for windows instance, supports SMB protocol and Windows NTFS
        3. Can be accessed outside fo AWS over SMB
    2. FSx for Lustre
        1. It's a type of parallel distributed file system.
        2. for large-scale cluster computing (ML, Analytics, etc.) on Linux
        3. Lustre = Linux + cluster
        4. Can be accessed outside fo AWS

20. Shared Responsibility Model for EC2
    1. YOU:
        1. Setting up snapshot/backup procedures
        2. Setting up data encryption
        3. The risk of using EC2 Instance Store
    2. AWS:
        1. Infrastructure
        2. Replication for data


## 4. Elastic Load Balancer and Auto Scaling Group
1. Term definition
    1. Scalability
        1. Vertical Scalability
            1. increase the size of the instance (same amount)
            2. common for non distributed system (e.g. database)
        2. Horizontal Scalability
            1. increase the number of instances
            2. for distributed system (e.g. web app)
            3. in EC2 you can use Auto Scaling Group and Load Balancer to achieve this
        3. A system can Auto-Scale also means it has Elasticity
        4. A system can scale fast and easily also means it has Agility
    2. Availability
        1. remain accessible to its users even when individual components fail
        2. in AWS means running system in at least 2 AZ
        3. Auto Scaling Group and Load Balancer can also achieve this
2. Elastic Load Balancer (ELB)
    1. Load balancing
        1. Servers that forward internet traffic to multiple server
        2. It spread load, do regular health check, and handle failure for instances
        3. Expense only single point of access
        4. Provide SSL termination (HTTPS)
    2. ELB
        1. Load balancer managed by AWS
        2. AWS take care of maintenance and availability
        3. It cost more compared to setup your own load balancer
    3. Kinds of load balancers offered by AWS
        1. Application (HTTP/HTTPS/gRPC)
            1. L7
            2. HTTP routing feature
            3. Static DNS (URL)
        2. Network (TCP/UTP)
            1. L4
            2. high performance
            3. Static IP through Elastic IP
        3. Gateway (GENEVE)
            1. L3
            2. Route traffic to third-party virtual appliances for analyze traffic first
            3. Send traffic to server after appliances say it's save
        4. Hands-On: ELB
            1. You can launch multiple instances at the same time when launch instances
            2. `EC2` > `Load balancers` > `Create load balancers`
            3. Application Load Balancer
                1. Listeners and routing > Forward to a target group
                2. `Create target group` > register instances to group
                3. Or manage target group in `EC2` > `Target groups`


3. Auto Scaling Group (ASG)
    1. It can scale out (add) or in (remove) EC2 instance automatically to match load
    2. It can replace unhealthy instances
    3. Automatically register new instance to a load balancer
    4. Hands-On: AGS
        1. `EC2` > `Launch Templates` > `Create launch template`
        2. Create a launch template is very similar to create an instance
        3. `EC2` > `Auto Scaling groups` > `Create Auto Scaling group`
            1. Choose launch template
            2. Choose instance launch options
                1. choose AZ
            3. Integrate with other services
                1. Attach to an existing load balancer
                2. Turn on Health checks
            4. Configure group size and scaling
                1. Desired capacity
                2. Min desired capacity
                3. Max desired capacity
    5. AGS Scaling strategies
        1. Manual update the size
        2. Dynamic scaling
            1. Simple/Step scaling
                1. when a CloudWatch alarm is triggered (e.g. CPU > 70) add instances
            2. Target Tracking scaling
                1. e.g. set the average CPU at 40%
            3. Scheduled Scaling
                2. set min capacity to 10 on Fridays
        3. Predicative Scaling
            1. Uses ML to predict future traffic
    6. Delete ASG will also terminate instances create by ASG


## 5. Simple Storage Service (S3)
1. S3 usa case
    1. back up and storage
    2. Application, Media hosting
    3. Data lake
    4. Software delivery
2. S3 Bucket
    1. store `Objects` (files) in `Bucket` (directories)
    2. Buckets must have **globally unique name** (across all regions)
    3. Buckets are defined at the **region level**
3. S3 Objects
    1. `Objects` have a key (FULL path)
    2. e.g. `s3://my-bucket/my_folder/my_file.txt`
        1. `my-bucket`: Bucket name
        2. `my_folder/my_file.txt`: Key
        3. `my_folder`: prefix
        4. `my_file.txt`: object name
    3. Object values are the content
        1. 5TB Max per Object
        2. 5GB per upload, use `multi-part upload`
    4. Metadata: list of text key/ value pairs
    5. Tags: unicode kry / value pair
    6. Version ID

4. S3 Security
    1. IAM based
        1. IAM Users/ User groups
        2. IAM Roles (for other AWS services)
    2. Bucket based
        1. Bucket Policies
            1. looks identical to IAM policies but its for bucket
            2. [see 2. Identity and Access Management (IAM)](#2-identity-and-access-management-iam)
            3. It can
                1. grant public access
                2. force objects to be encrypted at upload
                3. grant access to another account
        2. Object Access Control List
        3. Bucket Access Control List
        4. Bucket settings for Block Public Access
            1. You can block public access at Bucket settings
            2. This will prohibit public access even Bucket Policies say so.
    3. Encryption
        1. Server-Side Encryption (Default)
        2. Client-Side Encryption: Encrypt file before upload

5. S3 Versioning
    1. After Enable Bucket Versioning, delete or same  key overwrite will only create versions
    2. Delete a version to roll back

6. S3 Replication
    1. Can be in different AWS account
    2. Copy is asynchronous
    3. Must have proper IAM permission to S3
    4. Same-Region Replication
        1. for copy between production and test account
        2. for log aggregation
    5. Cross-Region Replication
        1. for compliance遵守
        2. for lower latency

7. S3 Storage classes
    1. Durability is 11 9's for all classes
    2. Availability depending on classes
    3. S3 Standard classes
        1. General Purpose
            1. 99.99% Availability
            2. Low latency and high throughput
            3. for Big Data, applications, content distribution, etc.
        2. Infrequent Access
            1. 99.9% Availability
            2. Lower cost
            3. for less frequently accessed, but can rapid access when needed
            4. for backups
    4. S3 One Zone Infrequent Access
        1. 99.5% Availability and store in a single AZ
        2. for secondary backup
    5. S3 Glacier classes
        1. low-cost storage fo archiving / backup
        2. pricing = storage cost + retrieval cost
        3. Instant Retrieval
            1. Millisecond retrieval time
            2. Minimum storage duration 90 days
        4. Flexible Retrieval
            1. Expedited (5 mins), Standard (5 hours), Bulk (12 hours) retrieval time
            2. Minimum storage duration 90 days
        5. Deep Archive
            1. Stander (12hours), Bulk (48 hours)
            2. Minimum storage duration 180 days
    6. S3 Intelligent Tiering
        1. pricing = storage cost + monthly monitoring + auto tiering
        2. Moves object automatically between tiers
            1. Frequent Access
            2. Infrequent Access: not accessed for 30 days
            3. Archive Instant Access: not accessed for 90 days
            4. Archive Access (Optional): 90 to 700+ days
            5. Deep Archive Access (Optional): 180 to 700+ days
    7. Storage classes is defined on each object.
    8. Lifecycle rules: custom rules to transition or delete objects


8. Hands-On: S3 
    1. Public access
        1. `S3` > select a bucket > `Permissions` 
        2. unblock public access settings
        3. `Bucket policy` > `Edit` > `AWS Policy Generator`
            1. Type of Policy > S3 Bucket Policy
    2. Static website hosting
        1. `S3` > select a bucket > `Properties` > `Static website hosting`
    3. Versioning
        1. `S3` > select a bucket > `Properties` > `Bucket Versioning`
        2. to permanently delete an object: select a bucket > `Objects` > turn on `Show version` > delete an object
    4. Replication
        1. `S3` > select a bucket > `Management` > Replication rules
    5. Storage classes
        1. Upload new objects: `S3` > select a bucket > `Upload` > `Properties`
        2. Existing objects: `S3` > select a bucket > select an object > `Properties` >  `Storage class`
    6. Create Lifecycle rules
        1. `S3` > select a bucket > `Management` > `Lifecycle configuration`

9. Shared Responsibility Model for EC2
    1. YOU:
        1. Versioning
        2. Bucket Policies
        3. Replication setup
        4. logging and monitoring
        5. Data encryption outside a Bucket
    2. AWS:
        1. Infrastructure

10. AWS Snowball
    1. A physical device for transferring a large amount of data. (Storage Optimized)
    2. It can also preprocess data at a edge. (Compute Optimized)
    3. pricing = device usage (days) + data transfer out of AWS

11. AWS Storage Gateway
    1. Bridge between on-premise本地端 data and AWS cloud
    2. for recovery, backup, etc.

## 6. Database and Analytics
1. Introduction
    1. Relational (SQL) Database
    2. Non Relational (NoSQL) Database
2. Amazon Relational Database Service (RDS)
    1. compare to deploying DB on EC2
        1. Automated provisioning and OS patching
        2. Easy backup and restore
        3. Monitoring
        4. Read replicas for improved performance
        5. Scalability
        6. Multi AZ
    2. You can not SSH into the RDS instance
    3. Amazon Aurora
        1. SQL optimized for cloud by AWS
        2. Compatible with MySQL or PostgreSQL
        3. Automatically scale up tp 128TB
        4. cost more, better performance
        5. Aurora DSQL: Serverless database
    4. Deployment option
        1. Read Replicas
            1. scale the read workload
            2. up to 15 replicas
            3. read from all replicas, write to main DB
        2. Multi-AZ
            1. increase availability
            2. it create a replica in different AZ
            3. can only have one other AZ replica
            4. only read and write to main DB
        3. Multi-Region
            1. for disaster recovery and reduce latency
            2. different regions read from different replicas, write to main DB
3. ElastiCache
    1. **in-memory** database, structure is similar to RDS
    2. reduce load off databases for read intensive workloads

4. DynamoDB
    1. NoSQL database
    2. It's distributed serverless database can scales to massive workload
    3. single-digit millisecond, low latency retrieval
    4. It's **key/value database**
        1. Primary Key: Partition Key + Sort Key (optional)
        2. Attributes
    2. DynamoDB Accelerator (DAX): in-memory DynamoDB
    3. Global Table
        1. make a DynamoDB table with low latency in multiple regions.
        2. it 2-way replication
        3. different regions read and write to different DB

5. Redshift
    1. **Data warehouses**
    2. based on PostgreSQL for online analytical processing (OLAP)
    3. Columnar storage
    4. have Massively Parallel Query Execution (MPP)
    5. integrate with BI tools such as AWS Quicksight ro Tableau
    6. Redshift Serverless

6. Other databases related servers in AWS
    1. Elastic MapReduce (EMR)
        1. helps create **Hadoop clusters** for Big Data
    2. Athena
        1. **Serverless** SQL service to perform analytic against **S3** object
        2. for BI, analyze logs
    3. Quicksight
        1. **Serverless** ML BI service to create interactive dashboards
        2. Integrate with lots of AWS databases
    4. DocumentDB
        1. NoSQL optimized for cloud by AWS
        2. Compatible with **mongoDB**
    5. Neptune
        1. **graph database**
        2. for knowledge graphs, social networking
    6. Timestream
        1. serverless **time series database**
    7. Managed Blockchain
        1. Compatible with Hyperledger Fabric and Ethereum
    8. AWS Glue
        1. serverless extract, transform, and load (ETL) service
    9. Database Migration Service (DMS)
        1. for database migration
            1. Homogeneous migration: to the same database structure (e.g. Oracle to Oracle)
            2. Heterogeneous: to the different database structure (e.g. Oracle to Aurora)

## 7. Other Compute services
1. Container services
    1. Elastic Container Service (ECS)
        1. for Docker on AWS
        2. You have to create EC2 first to let AWS manage and load balance container
    2. Fargate
        1. for Docker on AWS
        2. You not have to provision teh infrastructure (Serverless)
    3. Elastic Container Registry (ECR)
        1. Private Docker registry on AWS
    4. Elastic Kubernetes Service
        1. for Kubernetes on AWS
        2. Kubernetes can manage, deploy, and scaling Docker
        3. works on EC2 instance and Fargate
        4. Kubernetes is cloud-agnostic跨雲端的
2. Serverless services
    1. It starts form Function as a Service
    2. Now include anything that is managed
    3. e.g. S3, DynamoDB, Fargate, Lambda, etc.
    4. AWS Lambda
        1. no servers to manage (Serverless)
        2. for short execution
        3. run on-demand and event-Driven: invoke when needed
        4. automate scaling (CPU, RAM, Network, etc.)
        5. pricing: pay per request and compute time
        6. easy monitoring
    2. Amazon API Gateway
        1. for building a serverless API
3. AWS Batch
    1. for batch processing at any scale
    2. It will provision the right amount of EC2 instances or Spot instances (not serverless!)
    3. defined as Docker images (any runtime) and run on ECS

4. Amazon Lightsail
    1. for people with little cloud experience to use common cloud services
    2. limited integration with AWS

## 8. Deployment and Managing infrastructure
1. CloudFormation
    1. for outlining AWS infrastructure (most of services are support)
    2. Benefits
        1. infrastructure are controlled by code
        2. easy to estimate the costs and plan a saving strategy
        3. can be reconfigured on the fly
        4. automated generation of Diagram
        5. declarative programming
        6. leverage existing templates or documentation
    3. `CloudFormation` > `Application Composer`: to see the diagram
2. AWS Cloud Development Kit (CDK)
    1. Deploy infrastructure and application runtime code together
    2. The code is compiled into CloudFormation
3. AWS Elastic Beanstalk
    1. Platform as Service for developer
    2. It gathers common AWS infrastructure service in one view
    3. It managed instance, load balancing, auto-scaling, etc.
    4. It use CloudFormation in the background
    5. Hands-On
        1. `Elastic Beanstalk` > `Environments` > Create environment
            1. Configure environment
            2. Configure service access
                1. Create New Service IAM role
                2. Create New EC2 instance IAM role
                    1. ElasticBeanstalkMulticontainerDocker
                    2. ElasticBeanstalkWebTier
                    3. ElasticBeanstalkWorkerTier
4. AWS Systems Manager
    1. for manage EC2 and On-Premises system (Hybrid)
    2. important features
        1. patching automation
        2. run commands across servers
        3. store parameter configuration
    3. SSM Session Manager
        1. for start a secure shell on EC2 and On-Premises servers
        2. No SSH, bastion host, port 22 needed
        3. Can send session log to S3 or CloudWatch Logs
        4. use IAM role to allow Session Manager access EC2 (SSMManagedInstanceCore)
    4. SSM Parameter Store
        1. secure storage for configuration and secrets
        2. serverless

5. Developer services
    1. AWS CodeDeploy
        1. for automatic application deploy
        2. It can work with EC2 and on-premises servers (Hybrid)
    2. AWS CodeCommit
        1. code repository like GitHub
        2. already deprecate
    3. AWS CodeBuild
        1. compiles code, run test, and produces package
        2. serverless
    4. AWS CodePipeline
        1. for CI/CD
        2. Orchestrate the steps to automatically push code to production
        3. Compatible with AWS and 3re-party service (e.g. GitHub)
    5. AWS CodeArtifact
        1. artifact management service
        2. for storing and retrieving dependencies






