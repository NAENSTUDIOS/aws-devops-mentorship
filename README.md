# AWS DevOps Mentorship

[![AWS](https://img.shields.io/badge/AWS-Cloud%20Infrastructure-orange?logo=amazon-aws)](https://aws.amazon.com/)
[![Cloud Security](https://img.shields.io/badge/Focus-Cloud%20Security-1f6feb)](https://aws.amazon.com/security/)
[![Docker](https://img.shields.io/badge/Docker-Containerization-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Amazon ECS](https://img.shields.io/badge/Amazon%20ECS-Containers-FF9900?logo=amazon-aws)](https://aws.amazon.com/ecs/)
[![Amazon RDS](https://img.shields.io/badge/Amazon%20RDS-PostgreSQL-527FFF?logo=amazon-aws)](https://aws.amazon.com/rds/)
[![Amazon S3](https://img.shields.io/badge/Amazon%20S3-Replication-569A31?logo=amazon-aws)](https://aws.amazon.com/s3/)

## What this repository is

This is my working record from a DevOps Mentorship Program. It follows an application from Linux and AWS fundamentals through network design, container deployment, database integration, availability, and cross-region data protection.

The security objective is consistent throughout the work: understand where traffic is allowed, which identity can perform an action, where data is stored, how failures are handled, and how each decision can be validated.

## Progress

| Task | Subject | Status |
|---|---|---|
| [Task-1](Task-1/) | AWS fundamentals and Linux administration | Documented |
| [Task-2](Task-2/) | VPC, subnets, routing, IAM, security groups, and EC2 | Documented |
| [Task-3](Task-3/) | Containerized e-commerce deployment with ECR and ECS | Documented |
| [Task-4](Task-4/) | Production ECS service, Multi-AZ RDS, ALB, and S3 replication | Documented |
| Task-5 | Reserved for the next mentorship stage | Planned |
| Task-6 | Reserved for the next mentorship stage | Planned |
| Task-7 | Reserved for the next mentorship stage | Planned |

## Repository layout

```text
aws-devops-mentorship/
├── README.md
├── Task-1/
│   ├── README.md
│   └── screenshots/
├── Task-2/
│   ├── README.md
│   └── screenshots/
├── Task-3/
│   ├── README.md
│   ├── Commands.md
│   └── screenshots/
├── Task-4/
│   ├── README.md
│   ├── Commands.md
│   └── screenshots/
├── Task-5/
├── Task-6/
└── Task-7/
```

## Current technical scope

- Linux command-line administration and service control
- VPC segmentation, subnets, route tables, and internet connectivity
- IAM roles, policies, and least-privilege thinking
- Security-group traffic boundaries
- Docker image creation and private ECR distribution
- ECS service deployment and task redundancy
- PostgreSQL on Amazon RDS with Multi-AZ configuration
- Application Load Balancer validation
- S3 cross-region replication from Mumbai to Singapore
- Evidence-based troubleshooting with AWS CLI and ECS Exec

## Portfolio note

This repository is intentionally written as an engineering log, not a collection of generic cloud claims. Each completed task records the configuration that was used, the checks that were run, and the limitations of the available evidence. Screenshots for future tasks will be added when those tasks are completed.

## GitHub About

AWS DevOps mentorship portfolio focused on cloud infrastructure, container platforms, networking, identity, data protection, and practical cloud security.

## Topics

`aws` `devops` `cloud-security` `docker` `ecs` `ecr` `rds` `postgresql` `s3` `vpc` `iam` `linux` `infrastructure`
