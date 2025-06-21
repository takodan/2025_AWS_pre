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



## 2. IAM
1. Identity and Access Management
    1. Root account: shouldn't be used or shared 
    2. Users: can be grouped and be in multiple groups, but don't have to 
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