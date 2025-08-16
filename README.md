# Scalable Web Application with ALB and Auto Scaling

## Table of Contents
- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Deployment Guide](#deployment-guide)

---

## Overview
This project deploys a highly available and scalable web application on AWS using Amazon EC2, an Application Load Balancer (ALB), and an Auto Scaling Group (ASG). The application runs on EC2 instances placed in private subnets, while an internet-facing ALB distributes user traffic across them. The ASG automatically scales the number of instances based on demand, ensuring performance and cost efficiency.
Networking is built in a VPC across multiple Availability Zones for fault tolerance. Public subnets host the ALB and NAT Gateways, while private subnets host the EC2 instances. Security is enforced using IAM roles, security groups, and subnet isolation. Monitoring is handled by Amazon CloudWatch with alerts delivered through Amazon SNS.
This architecture ensures resilience, scalability, and secure operations while following AWS best practices.
 

![Architecture Diagram]<img width="1156" height="640" alt="architecture-diagram" src="https://github.com/user-attachments/assets/43130c79-a68e-4f80-a6b8-97bf10e91ad8" />


---

## Architecture
The solution includes the following AWS services:

- **Amazon VPC**: Custom VPC with public and private subnets across multiple Availability Zones.  
- **Application Load Balancer (ALB)**: Internet-facing entry point distributing traffic across EC2 instances.  
- **Auto Scaling Group (ASG)**: Ensures EC2 instances scale up/down based on demand.  
- **Amazon RDS**: Provides a managed, highly available database.  
- **AWS IAM**: Role-based access for EC2 to securely fetch secrets from AWS Secrets Manager.  
- **Amazon CloudWatch + SNS**: Metrics, alarms, and email notifications for proactive monitoring.  

---

## Features
- High availability across multiple AZs.  
- Automatic scaling based on CPU utilization.  
- Secure architecture with private subnets and IAM roles.  
- Centralized monitoring and alerting via CloudWatch & SNS.  
- Cost-efficient design with scaling policies and optimized instance types.  

---

## Deployment Guide
Look at the documentaion for more details
## Deployment Steps

1. **Create a VPC**  
   - Configure 2 public and 4 private subnets across two Availability Zones with two NAT gateways on per AZ.  

2. **Configure Security Groups**  
   - ALB SG: Allow inbound HTTP/HTTPS from the internet.  
   - EC2 SG: Allow inbound traffic only from the ALB SG.  
   - RDS SG : Allow inbound traffic only from the EC2 SG.  

3. **Deploy RDS Database**  
   - Launch RDS in private subnets.  
   - Configure connectivity and set up security rules.  

4. **Launch an EC2 Instance**  
   - Install and configure the web application.  
   - Create an AMI from the configured instance.  

5. **Create a Launch Template**  
   - Use the AMI as the base image.  
   - Attach IAM role required.  

6. **Create an Auto Scaling Group (ASG)**  
   - Distribute instances across private subnets in multiple AZs.  
   - Configure scaling policies (CPU threshold, desired/min/max).  

7. **Deploy an Application Load Balancer (ALB)**  
   - Place in public subnets.  
   - Connect target group to the ASG.  

8. **Configure Monitoring & Alerts**  
    - Configure Composite Alarm (e.g., CPU > 70% AND ASG at max capacity).  
    - Connect alarms to an SNS topic for email notifications.  

### Prerequisites
- AWS Account with admin privileges.  



