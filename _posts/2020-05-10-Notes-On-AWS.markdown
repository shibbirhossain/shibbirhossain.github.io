---
layout: post
title:  "Notes On AWS"
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


