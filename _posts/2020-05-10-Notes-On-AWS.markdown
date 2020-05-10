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

