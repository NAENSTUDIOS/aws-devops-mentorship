# Task-2 — AWS Infrastructure Foundation

## Objective

Design and validate the network, identity, and compute foundation required for secure application workloads on AWS.

## Infrastructure Built

### VPC and subnets

- Created a VPC with a defined CIDR range.
- Configured public and private subnets.
- Enabled DNS settings required by the workload.

### Internet connectivity and routing

- Attached an Internet Gateway.
- Configured route tables for public access.
- Associated the appropriate subnets with their route tables.

### Security groups

Defined access rules for:

- HTTP on port `80`
- HTTPS on port `443`
- SSH on port `22`
- Application traffic where required

The design principle was to allow only the traffic needed by each tier rather than expose every resource broadly.

### IAM

- Created IAM users, roles, and policies.
- Applied least-privilege access as the operating principle.
- Separated human access from workload permissions.

### EC2

- Launched an Amazon Linux instance.
- Associated the instance with a security group.
- Configured user access.
- Validated reachability and administration using `ssh`, `ping`, and `curl`.

### Application endpoint

The production Application Load Balancer endpoint supplied for this environment is:

```text
http://prod-alb-1957656459.ap-south-1.elb.amazonaws.com
```

This endpoint is the public HTTP entry point for the application path. It should be tested with `curl` after confirming that the ALB listener, target group, security group, and backend service are ready.

## Architecture

```text
Internet user
    |
    v
Application Load Balancer
    |
    v
VPC
  +---+---+
  |       |
Public  Private
Subnet  Subnet
  |
  v
EC2 instance
```

## Security Focus

Task 2 introduced the controls that later support the ECS and RDS deployment:

- Network segmentation between public and private areas.
- Explicit ingress rules through security groups.
- IAM roles and policies instead of embedding access keys in workloads.
- SSH used for administration and restricted through security-group rules.
- Connectivity tested from the actual instance environment.

## Validation

```bash
ping <host>
curl http://prod-alb-1957656459.ap-south-1.elb.amazonaws.com
ssh <user>@<host>
```

## Learning Outcomes

- Designed a basic AWS network boundary.
- Distinguished public and private subnet use cases.
- Connected routing decisions to security outcomes.
- Configured IAM access with least privilege in mind.
- Launched and administered an EC2 instance.
- Built the infrastructure vocabulary needed for production container platforms.

## Screenshots

Screenshots will be added to `Task-2/screenshots/` when the Task-2 evidence set is uploaded.

```text
Task-2/screenshots/
├── vpc-overview.png
├── subnets.png
├── route-table.png
├── security-groups.png
├── iam-role.png
└── ec2-instance.png
```
