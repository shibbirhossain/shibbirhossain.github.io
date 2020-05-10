---
layout: post
title:  "Study Notes On AWS"
date:   2020-05-10 06:36:00 +1100
categories: [blog, tech]
tags: [AWS, notes, developer]
comments: true
---
![aws](/assets/aws.svg){: .center-image }  
  

### IAM
* SAML(Security Assertion Markup Language 2.0)  
    Enables users to access AWS resources with their corporate credentials. _Ex:_ Active Directory
* It is recommended to have 1 IAM role per application

### EC2
* EBS - Elastic block store, virtual drive
* ELB - distributing load accross
* ASG - Scaling the services  

subnet - which AZ  
tags - Name (going to show in UI)  
EC2 connect - ssh from browser (AMI linux 2 only)  
pem file permission - 0644 -> too open  
> chmod 0400 *.pem  

### Load Balancers
* HTTPS (SSL termination)
* Enforce stickiness with cookies  

Three diff kinds of LB offerings:
1. Classic Load Balancer 
2. Application Load Balancer - HTTP/HTTPS (L7)
3. Network Load Balancer - TCP (L4)  

To get the actual IP 
> x-forwarded-for (contains the actual IP)

### ASG
* Min Size
* Actual Size / Desired Capacity
* Max Size  

Send Custom Metric via --> PutMetric API  
> ASG <- -triggered by- - cloudWatch  

ASG uses Launch Configuration

### EBS Volume 
Network drive (not physical drive),attach to AZ, EBS encryption  
In flight and at rest encryption  
Snapshots are also encrypted

## Route 53
* A - URL to IPV4
* AAAA - URL to IPV6
* CNAME - URL to URL 
* ALIAS - URL to AWS Resources

## RDS 
* Encryption at rest - KMS - **AES-256**
* Encryption in flight - **SSL**
    * postgres - rds.force_ssl = 1
    * MySQL - REQUIRE SSL

## ElastiCache
Redis/Memcached
* make application stateless by storing state in a common cache
* Write scaling - Sharding
* Read scaling - Read replicas
* multi AZ with failover
* cache hit / cache miss
* cache invalidation strategy  
    
#### Redis     
1. in memory **Key-value**
2. super low latency (sub micro sec)
3. cache survive reboots by default (persistence)
4. great to host -   
                i) user sessions  
                ii) Leaderboard  
                iii) distributed states  
                iv) relieve pressure on db  
                v) pub/sub messaging  

#### Memcached
1. in memory **object** store
2. cache doesn't survive reboots

#### Elasticache Patterns
1. Lazy loading  
    Pros:  
    * only requested data is cached
        
    Cons:
    * cache miss penalty  
    * Stale data - to avoid this use Write-Through and TTL strategy  

2. Write through  
    Pros:  
    * cache is never stale
    * write penalty as oppose to read penalty: users are more tolerant when uploading data

    Cons:
    * cache churn : waste of resource, most data is never read.  


### S3 Versioning
best practice is to enable versioning
* protect against unintended delete
* easy rollback to prev version

### S3 Encryption
1. SSE-S3 - managed by AWS S3
2. SSE-KMS - managed by AWS KMS
3. SSE-C - you want to manage your own encryption key (BYO encryprion Key)
4. Client Side encryption

#### SSE-S3
AWS S3 manages, object encrypted server side  
AES-256 encryption type  
Must set Header:   
> "x-amz-server-side-encryption": "AES-256"  

#### SSE-KMS
managed by AWS KMS  
Pro:
* user control + audit trail (key rotation)

Server side enc
Header:  
> "x-amz-server-side-encryption": "aws:kms" 

Key -  KMS Customer Master Key (CMK)

#### SSE-C
* fully managed by customer outside of AWS
* S3 does not store the encryption key
* must use HTTPS
* encryption key must be provided in HTTP header
* Key - Client side data key

#### Client Side encryption
* Client library such as S3 Encryption Client
* Client must encrypt the data themselves before sending to S3
* Client must decrypt data themselves when retrieving from S3
* Customer manages key + encryption cycle

#### Encryption in Transit(SSL/TLS) - In flight
* SSE-C in HTTPS is must
* SSL/TLS





