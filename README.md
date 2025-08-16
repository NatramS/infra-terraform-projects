# Terraform AWS Multi-Tier Architecture

## Project Overview
This project provisions a **highly available multi-tier architecture** on AWS using Terraform.  
It includes the following components:
- **VPC** with public and private subnets across multiple AZs.
- **Internet Gateway** and **NAT Gateway** for external connectivity.
- **Application Load Balancer (ALB)** in public subnets.
- **EC2 Auto Scaling Group** in private subnets for application servers.
- **RDS MySQL Database** in private subnets.
- **Security Groups** to enforce least-privilege access.

## Architecture Diagram
```
                Internet
                   |
             [ Application Load Balancer ]
                   |
          -----------------------------
          |                           |
      [ EC2 - App Server ]       [ EC2 - App Server ]
          |                           |
          ----------- Private Subnet -----------
                         |
                   [ RDS MySQL DB ]
```
## Project Structure

multi-tier-aws-terraform/
|-- main.tf                # Root module – calls VPC, EC2, RDS, ALB
|-- variables.tf           # Input variables
|-- outputs.tf             # Outputs (ALB DNS, DB endpoint, etc.)
|-- terraform.tfvars       # Variable values (not committed)
|-- modules/
|   |-- vpc/               # VPC, subnets, IGW, NAT
|   |   |-- main.tf
|   |   |-- variables.tf
|   |   `-- outputs.tf
|   |-- ec2/               # Launch template, ASG
|   |   |-- main.tf
|   |   |-- variables.tf
|   |   `-- outputs.tf
|   |-- alb/               # Application Load Balancer
|   |   |-- main.tf
|   |   |-- variables.tf
|   |   `-- outputs.tf
|   `-- rds/               # RDS MySQL DB
|       |-- main.tf
|       |-- variables.tf
|       `-- outputs.tf
`-- README.md              # Documentation

## Getting Started

### 1. Prerequisites
- AWS account with IAM user (programmatic access).
- Terraform installed (>= 1.3).
- AWS CLI installed & configured.

### 2. Clone Repository
```bash
git clone https://github.com/yourusername/multi-tier-aws-terraform.git
cd multi-tier-aws-terraform
```

### 3. Initialize Terraform
```bash
terraform init
```

### 4. Plan Deployment
```bash
terraform plan
```

### 5. Apply Deployment
```bash
terraform apply -auto-approve
```

### 6. Destroy Deployment
```bash
terraform destroy -auto-approve
```

## Inputs
| Variable       | Description                  | Default         |
|----------------|------------------------------|-----------------|
| region         | AWS region to deploy         | us-east-1       |
| instance_type  | EC2 instance type            | t2.micro        |
| db_username    | RDS DB username              | admin           |
| db_password    | RDS DB password              | (set in tfvars) |

## Outputs
- **ALB DNS Name** → Access your application via the load balancer.

## Future Improvements
- Add HTTPS with ACM + ALB (port 443).
- CI/CD integration with AWS CodePipeline.
- Auto Scaling policies for application servers.
- Centralized logging & monitoring with CloudWatch.

---
Author: Sharath Natram  
LinkedIn: [linkedin.com/in/sharathnatram-cloud-devops](https://linkedin.com/in/sharathnatram-cloud-devops)
