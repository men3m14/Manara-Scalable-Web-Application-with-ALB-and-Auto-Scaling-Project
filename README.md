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
 

![Architecture Diagram]![WhatsApp Image 2025-08-16 at 14 20 23_7fda11c7](https://github.com/user-attachments/assets/d26dccaf-14e4-42e4-bf84-5d12f08feac5)



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
      <img width="975" height="341" alt="image" src="https://github.com/user-attachments/assets/0014580b-479e-4ff7-b926-e8b9fb83ce0e" />


2. **Configure Security Groups**  
   - ALB SG: Allow inbound HTTP/HTTPS from the internet.
      <img width="975" height="313" alt="image" src="https://github.com/user-attachments/assets/c0b477c0-d65e-4a5d-8a96-ceffb7f73e83" />
   - EC2 SG: Allow inbound traffic only from the ALB SG.
      <img width="975" height="343" alt="image" src="https://github.com/user-attachments/assets/62ee24eb-0f7e-4783-9567-729b65e21dc4" />
   - RDS SG : Allow inbound traffic only from the EC2 SG.
      <img width="975" height="346" alt="image" src="https://github.com/user-attachments/assets/98b175e1-9273-4167-be58-52e005325a42" />


3. **Deploy RDS Database**  
   - Launch RDS in private subnets.  
   - Configure connectivity and set up security rules.
      ![WhatsApp Image 2025-08-16 at 15 01 09_c44e30c8](https://github.com/user-attachments/assets/c00e8c45-ef5b-496f-ba73-b4a6d9f0c1b6)


4. **Launch an EC2 Instance**  
   - Install and configure the web application.
      <img width="975" height="252" alt="image" src="https://github.com/user-attachments/assets/557ab551-2c83-485c-b700-55dc10c633ca" />
   -  Create an AMI from the configured instance.
      <img width="975" height="211" alt="image" src="https://github.com/user-attachments/assets/a4d9598e-abea-4baa-bb52-8cda42155ba2" />

5. **Create a Launch Template**  
   - Use the AMI as the base image.
       ![WhatsApp Image 2025-08-16 at 14 48 23_64bd5877](https://github.com/user-attachments/assets/658bf4c2-8d21-44f6-a129-3f58b49c694f)
   - Attach IAM role required.
       ![WhatsApp Image 2025-08-16 at 14 48 24_4709cf74](https://github.com/user-attachments/assets/a8f6ccfc-e355-458b-afa9-3c0fef8df15e)

6. **Create an Auto Scaling Group (ASG)**  
   - Distribute instances across private subnets in multiple AZs.  
   - Configure scaling policies (CPU threshold, desired/min/max).
       ![WhatsApp Image 2025-08-16 at 14 48 30_8ed37010](https://github.com/user-attachments/assets/16437ba7-9b4b-4cf2-8e88-68811f5f4b5b)

7. **Deploy an Application Load Balancer (ALB)**
   - Connect target group to the ASG.
       ![WhatsApp Image 2025-08-16 at 14 59 05_6b4eb345](https://github.com/user-attachments/assets/ced1d564-f55f-4532-baf6-425b631d879d)
   - Place in public subnets.
       ![WhatsApp Image 2025-08-16 at 14 59 03_2cf42c6f](https://github.com/user-attachments/assets/320cbd4f-3c7a-4c73-be73-40df76ffb7c8)

9. **Configure Monitoring & Alerts**
    - Create SNS topic for email notifications.
       <img width="975" height="314" alt="image" src="https://github.com/user-attachments/assets/bbab65b5-65cc-4751-bb4a-102123d24731" />
    - Configure Composite Alarm (e.g., CPU > 70% AND ASG at max capacity).  
       ![WhatsApp Image 2025-08-16 at 15 10 15_a8a392fb](https://github.com/user-attachments/assets/aeeba95a-13ba-4b1b-8366-9ba2a81cc0eb)

10.**The Result**
        <img width="975" height="510" alt="image" src="https://github.com/user-attachments/assets/8c3290dc-4acc-46d6-a5c5-7bd2f9095466" />




