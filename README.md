# Ansible AWS foundations

A minimal, modular Ansible project for provisioning foundational AWS infrastructure.
It starts with a fully automated **VPC + subnet setup** and can be extended with EC2, S3, IAM, and CloudFormation components.

> ✅ AWS ready
> 🔁 Idempotent via Ansible
> ☁️ Uses official `amazon.aws` collection

---

## Overview

This repository automates baseline AWS infrastructure creation using Ansible and boto3 modules.
You can deploy networking primitives (VPC, subnets, route tables, gateways) in minutes from your local environment.

The structure is designed to be readable, extensible, and ready for additional modules (EC2, IAM, S3, etc.).

---

## 📁 Project Layout

```
ansible-aws-foundations/
├── inventory/
│   └── aws_ec2.yml              # Dynamic inventory (AWS API)
├── roles/
│   ├── vpc/
│   │   ├── tasks/main.yml       # Create VPC, subnets, routes, IGW
│   │   └── vars/main.yml        # Default CIDRs and tags
│   ├── ec2/
│   │   └── tasks/main.yml       # Launch EC2 instances (optional)
│   ├── s3/
│   │   └── tasks/main.yml       # Create S3 buckets (optional)
│   └── iam/
│       └── tasks/main.yml       # Create IAM roles/policies (optional)
├── playbooks/
│   └── provision.yml            # Entry point
├── group_vars/
│   └── all.yml                  # AWS credentials, region, tags
├── requirements.txt             # boto3, botocore, ansible
└── README.md
```

---

## 🚀 Usage

1. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ansible-galaxy collection install amazon.aws
   ```

2. **Configure credentials**
   Export your AWS credentials or set them in `group_vars/all.yml`:

   ```yaml
   aws_region: eu-west-1
   aws_access_key: YOUR_ACCESS_KEY
   aws_secret_key: YOUR_SECRET_KEY
   ```

3. **Run the playbook**

   ```bash
   ansible-playbook playbooks/provision.yml
   ```

4. **Verify resources**

   ```bash
   aws ec2 describe-vpcs --region eu-west-1
   ```

---

## 🧩 Example Variables

```yaml
vpc_name: "demo-vpc"
vpc_cidr: "10.0.0.0/16"
subnets:
  - cidr: "10.0.1.0/24"
    az: "eu-west-1a"
  - cidr: "10.0.2.0/24"
    az: "eu-west-1b"
tags:
  Project: ansible-aws-foundations
  Environment: dev
```

---


