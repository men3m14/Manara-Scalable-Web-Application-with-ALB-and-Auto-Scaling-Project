# Scalable Web Application with ALB and Auto Scaling

## Table of Contents
- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Deployment Guide](#deployment-guide)
  - [Steps](#steps)
- [Monitoring & Alerts](#monitoring--alerts)

---

## Overview
This project deploys a **highly available and scalable web application** on AWS using **Amazon EC2**, **Application Load Balancer (ALB)**, and **Auto Scaling Groups (ASG)**.  
The architecture ensures **fault tolerance, elasticity, and cost optimization**.  
Optional integration with **Amazon RDS** provides a managed relational database backend.  

![Architecture Diagram](<img width="1156" height="640" alt="architecture-diagram" src="https://github.com/user-attachments/assets/43130c79-a68e-4f80-a6b8-97bf10e91ad8" />
)

---

## Architecture
The solution includes the following AWS services:

- **Amazon VPC**: Custom VPC with public and private subnets across multiple Availability Zones.  
- **Application Load Balancer (ALB)**: Internet-facing entry point distributing traffic across EC2 instances.  
- **Auto Scaling Group (ASG)**: Ensures EC2 instances scale up/down based on demand.  
- **Amazon RDS (Optional)**: Provides a managed, highly available database.  
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

### Prerequisites
- AWS Account with admin privileges.  
- AWS CLI installed and configured.  
- (Optional) GitHub Actions or CI/CD pipeline for automation.  

### Steps

