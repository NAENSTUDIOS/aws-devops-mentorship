# Task 4 Commands

These commands are limited to actions visible in the supplied screenshots or directly required to reproduce the documented validation. Replace placeholders with environment-specific values and never commit credentials.

## AWS CLI Commands

Set the deployment region:

```bash
export AWS_REGION=ap-south-1
```

Inspect the ECS cluster:

```bash
aws ecs describe-clusters \
  --clusters ecom-cluster \
  --region "$AWS_REGION"
```

Inspect the ECS service and task counts:

```bash
aws ecs describe-services \
  --cluster ecom-cluster \
  --services e-com-service \
  --region "$AWS_REGION"
```

List running service tasks:

```bash
aws ecs list-tasks \
  --cluster ecom-cluster \
  --service-name e-com-service \
  --desired-status RUNNING \
  --region "$AWS_REGION"
```

## ECS Commands

Open an interactive shell inside the running application container:

```bash
aws ecs execute-command \
  --cluster ecom-cluster \
  --task <task-id> \
  --container app \
  --interactive \
  --command "/bin/sh" \
  --region ap-south-1
```

The supplied validation used the `app` container and an ECS Exec session.

## RDS Commands

The first validation attempt used `psql`:

```bash
psql \
  -h <RDS-ENDPOINT> \
  -U appuser \
  -d shop \
  -c "SELECT COUNT(*) FROM products;"
```

The container reported `psql: not found`. The successful validation used the Node.js PostgreSQL client from inside the ECS task:

```bash
node -e "const {Client}=require('pg'); const c=new Client({host:'<RDS-ENDPOINT>',port:5432,user:'appuser',password:'<DB-PASSWORD>',database:'shop'}); c.connect().then(()=>c.query('SELECT COUNT(*) FROM products')).then(r=>{console.log('count =',r.rows[0].count); c.end()});"
```

Expected result from the supplied screenshot:

```text
count = 12
```

## S3 Commands

Upload the test object to the Mumbai bucket:

```bash
aws s3 cp test-file.txt \
  s3://ecom-uploads-mumbai-584860296694/test-file.txt \
  --region ap-south-1
```

List the Mumbai bucket:

```bash
aws s3 ls \
  s3://ecom-uploads-mumbai-584860296694 \
  --region ap-south-1
```

List the Singapore bucket:

```bash
aws s3 ls \
  s3://ecom-uploads-singapore-584860296694 \
  --region ap-southeast-1
```

Inspect the Mumbai bucket replication configuration:

```bash
aws s3api get-bucket-replication \
  --bucket ecom-uploads-mumbai-584860296694 \
  --region ap-south-1
```

## Load Balancer Validation

Request the application through the ALB:

```bash
curl http://ecom-alb-new-56207691.ap-south-1.elb.amazonaws.com
```

The supplied output returned the Shop application HTML.

## Validation Commands

Check ECS service state:

```bash
aws ecs describe-services \
  --cluster ecom-cluster \
  --services e-com-service \
  --query 'services[0].{desired:desiredCount,running:runningCount,pending:pendingCount,status:status}' \
  --region ap-south-1
```

Confirm the RDS instance is available:

```bash
aws rds describe-db-instances \
  --db-instance-identifier ecomdb \
  --query 'DBInstances[0].{status:DBInstanceStatus,engine:Engine,multiAZ:MultiAZ,port:Endpoint.Port}' \
  --region ap-south-1
```

Confirm the uploaded object exists:

```bash
aws s3api head-object \
  --bucket ecom-uploads-mumbai-584860296694 \
  --key test-file.txt \
  --region ap-south-1
```

## Troubleshooting Commands

Review recent ECS service events:

```bash
aws ecs describe-services \
  --cluster ecom-cluster \
  --services e-com-service \
  --query 'services[0].events[:10]' \
  --region ap-south-1
```

Inspect a specific task:

```bash
aws ecs describe-tasks \
  --cluster ecom-cluster \
  --tasks <task-id> \
  --region ap-south-1
```
