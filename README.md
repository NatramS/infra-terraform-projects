# Terraform AWS Multi-Tier Infrastructure

This project provisions a **highly available multi-tier architecture** on AWS using Terraform.  
It includes a VPC, subnets, Internet/NAT Gateways, an Application Load Balancer, EC2 instances for the app layer, and an RDS MySQL database.

---

## Architecture Overview

                ┌───────────────────────────┐
                │        Internet           │
                └─────────────┬─────────────┘
                              │
                   ┌──────────▼───────────┐
                   │ Application Load     │
                   │ Balancer (ALB)       │
                   └──────────┬───────────┘
                              │
             ┌────────────────┴────────────────┐
             │                                 │
   ┌─────────▼─────────┐             ┌─────────▼─────────┐
   │ EC2 Instance 1     │             │ EC2 Instance 2     │
   │ (App Server)       │             │ (App Server)       │
   └─────────┬─────────┘             └─────────┬─────────┘
             │                                 │
             └─────────────────┬───────────────┘
                               │
                     ┌─────────▼─────────┐
                     │   RDS MySQL DB    │
                     │ (Private Subnet)  │
                     └───────────────────┘


---

## Features

- Custom **VPC** with public & private subnets across 2 AZs  
- **Internet Gateway + NAT Gateway** for public/private traffic flow  
- **Application Load Balancer (ALB)** with target groups  
- **Auto-scalable EC2 instances** for the web tier  
- **RDS MySQL** in private subnets for persistence  
- **Security Groups** enforcing least-privilege access  

---

## Project Structure

multi-tier-aws-terraform/
│── main.tf # Root Terraform configuration
│── variables.tf # Input variables
│── outputs.tf # Exported outputs
│── vpc.tf # VPC, subnets, gateways
│── security-groups.tf # Security groups
│── alb.tf # Load balancer configuration
│── ec2.tf # EC2 instances + autoscaling
│── rds.tf # RDS database
│── provider.tf # AWS provider configuration
│── README.md # Documentation

## 🚀 Deployment Steps

### 1️⃣ Prerequisites
- AWS Account  
- Terraform ≥ 1.3  
- AWS CLI configured (`aws configure`)  
- SSH key pair in AWS (for EC2 access)  

### 2️⃣ Clone the Repo
```bash
git clone https://github.com/your-username/multi-tier-aws-terraform.git
cd multi-tier-aws-terraform

Initialize Terraform
terraform init

Validate & Plan
terraform validate
terraform plan -out=tfplan

Apply the Infrastructure
terraform apply tfplan

Destroy (when no longer needed)
terraform destroy

Variables

<img width="876" height="447" alt="image" src="https://github.com/user-attachments/assets/0309e9b5-7aaf-43d9-a73d-0c01cf1f5b60" />


Outputs

alb_dns_name → DNS name of the Application Load Balancer
db_endpoint → RDS endpoint
Next Steps / Improvements
Add ACM SSL certificates for HTTPS on ALB
Integrate with AWS CodePipeline for CI/CD automation
Add CloudWatch monitoring & alarms
Enable Auto Scaling Groups for EC2 layer
Add S3 + CloudFront for static content delivery


