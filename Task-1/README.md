# Task-1 — AWS Fundamentals and Linux Administration

## Objective

Build the AWS and Linux foundation required to operate cloud infrastructure safely from the command line.

## Scope

### AWS fundamentals

- Cloud computing concepts
- AWS global infrastructure
- Regions and Availability Zones
- The AWS shared responsibility model
- AWS Management Console navigation

### Linux administration

- File and directory management
- Users and permissions
- Package installation
- Service management with `systemctl`
- Log inspection
- Command-line operations

### Networking fundamentals

- Basic reachability checks with `ping`
- HTTP testing with `curl`
- Socket and connection inspection with `netstat` and `ss`

## Commands Practised

```bash
pwd
ls -la
cd
mkdir
rm
cp
mv
cat
nano
sudo su -
systemctl status
systemctl start
systemctl stop
systemctl restart
ping
curl
netstat
ss
```

## Security Relevance

This task established the operational habits used later in the repository: work from the command line, verify service state instead of assuming it, inspect network behaviour, and understand the boundary between AWS-managed controls and customer-managed configuration.

## Learning Outcomes

- Navigated AWS Regions and Availability Zones with an infrastructure mindset.
- Used Linux commands to inspect and modify a server environment.
- Managed services and checked their state with `systemctl`.
- Applied basic network diagnostics before escalating a connectivity problem.
- Built the baseline needed for IAM, VPC, EC2, and container operations.

## Screenshots

Screenshots will be added to `Task-1/screenshots/` when the Task-1 evidence set is uploaded.

```text
Task-1/screenshots/
├── aws-console.png
├── linux-terminal.png
├── file-management.png
└── system-services.png
```
