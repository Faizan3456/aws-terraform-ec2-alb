# AWS EC2 Deployment Behind Application Load Balancer (Terraform)

## Overview
This project demonstrates deploying **multiple AWS EC2 instances behind an Application Load Balancer (ALB)** using **Terraform (Infrastructure as Code)**.  
Apache web servers are installed automatically on each instance, and traffic is distributed through the ALB.

The infrastructure is **secure, scalable, reproducible, and fully automated**.

---

## Purpose
The purpose of this project is to demonstrate hands-on experience with:
- Infrastructure as Code using Terraform
- High availability using AWS Application Load Balancer
- Secure networking and traffic management
- Automated server configuration using `user_data`

This project reflects real-world cloud architecture patterns used in production environments.

---

## Architecture
- AWS Application Load Balancer (ALB)
- Multiple AWS EC2 instances (Amazon Linux 2023)
- Target Group with health checks
- Security Groups
  - HTTP (80) allowed from the internet
  - SSH (22) restricted to my public IP
- Default VPC and subnets
- Terraform (Infrastructure as Code)

---

## Terraform Resources
- `aws_lb` – Application Load Balancer  
- `aws_lb_target_group` – Target group for EC2 instances  
- `aws_lb_listener` – HTTP listener  
- `aws_instance` – EC2 instances  
- `aws_security_group` – Network security rules  
- `aws_ami` (data source) – Amazon Linux 2023 AMI  
- `aws_vpc` (data source) – Default VPC  
- `aws_subnets` (data source) – Default subnets  

---

## How It Works
1. Terraform initializes the AWS provider  
2. Retrieves the latest Amazon Linux 2023 AMI  
3. Creates security groups for ALB and EC2 instances  
4. Launches multiple EC2 instances  
5. Installs Apache on each instance using `user_data`  
6. Creates an Application Load Balancer  
7. Registers EC2 instances in a target group  
8. Routes traffic via the ALB listener  
9. Outputs ALB DNS name and EC2 public IPs  

---

## Inputs
```hcl
aws_region     = "eu-north-1"
my_ip_cidr     = "YOUR_PUBLIC_IP/32"
key_name       = "YOUR_EXISTING_EC2_KEYPAIR"
instance_count = 2
```
-------
## Output

alb_dns_name = "tf-web-alb-597720456.eu-north-1.elb.amazonaws.com"
alb_url      = "http://tf-web-alb-597720456.eu-north-1.elb.amazonaws.com"
instance_public_ips = [
  "16.170.220.215",
  "16.170.207.12"
]


## Screenshots

<img width="921" height="421" alt="ALB serving EC2 traffic" src="https://github.com/user-attachments/assets/5d139178-1e6e-4661-bc21-51e84bef9e3d" /> 

-----
## Usage 

1. terraform init
2. terraform validate
3. terraform plan
4. terraform apply

-------

## Cleanup

1. terraform destroy



