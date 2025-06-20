# AWS Certified Cloud Practitioner
## 0. resresource
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
    1. Trade capita; expense (CAPEX) for operational expense (OPEX)
        - reduced Total Cost of Ownership (TCO)& Operational Expense (OPEX)
    2. Benefit from massive economies of scale
    3. stop gussing capacity
    4. increase speed and agility
    5. Stop spending money running and maintaining data centers
    6. Go blobal in minutes

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