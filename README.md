# three--tier--ecommerce--aws
Production-style Three-Tier E-Commerce Web App on AWS using EC2, ALB, RDS (MySQL), and S3, with custom VPC networking, public/private subnets, and CloudWatch monitoring.
# three--tier--ecommerce--aws

Production-style Three-Tier E-Commerce Web App infrastructure on AWS using EC2, ALB, 
RDS (MySQL), and S3, with custom VPC networking, public/private subnets, and CloudWatch 
monitoring.

## Architecture
- **Presentation Tier:** Application Load Balancer (ALB) distributing traffic across 
  EC2 instances in a target group
- **Application Tier:** EC2 instances (t3.micro) running Apache, deployed across two 
  Availability Zones (ap-south-1a, ap-south-1b) for high availability
- **Data Tier:** Amazon RDS (MySQL) for the database, S3 bucket for product image storage
- **Monitoring:** CloudWatch alarms (EC2 CPU utilization, target group unhealthy hosts) 
  with SNS email notifications for alerting

## Networking & Security
- Custom VPC (10.0.0.0/16) with 4 subnets — public and private across two AZs
- Route tables, Internet Gateway, and NAT Gateways for public/private traffic separation
- Security Groups scoped per tier: ALB, EC2, and RDS each have dedicated rules
- IAM: custom least-privilege policy granting EC2 scoped access to the S3 bucket 
  (List, Read, Write only — not full S3 access)

## Current Status
Infrastructure is fully provisioned and healthy — ALB routes to 2 healthy EC2 targets, 
RDS is available, CloudWatch alarms are active. EC2 instances currently serve the Apache 
default page as a placeholder; application code deployment is a planned next step.

## Tech Stack
AWS (VPC, EC2, ALB, RDS, S3, IAM, CloudWatch, SNS), Apache, MySQL

## What I Learned
- Designing secure, multi-tier network architecture across multiple Availability Zones
- Configuring least-privilege IAM policies instead of broad permissions
- Setting up proactive monitoring and alerting rather than just reactive troubleshooting