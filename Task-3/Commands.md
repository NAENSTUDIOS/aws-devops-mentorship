# Task 3 Commands

The commands below are limited to the Docker, ECR, ECS, RDS, troubleshooting, and validation actions directly shown or strongly supported by the Task 3 evidence.

## AWS CLI Commands

Set the deployment region and account-specific registry values:

```bash
export AWS_REGION=ap-south-1
export AWS_ACCOUNT_ID=<account-id>
export ECR_REPOSITORY=e-com-app
export ECR_REGISTRY=${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com
```

Authenticate Docker with the private ECR registry:

```bash
aws ecr get-login-password --region "$AWS_REGION" \
  | docker login --username AWS --password-stdin "$ECR_REGISTRY"
```

## Docker Commands

Build the application image:

```bash
docker build -t ecommerce-app .
```

Inspect locally created images:

```bash
docker images
```

Tag the image for ECR:

```bash
docker tag ecommerce-app:latest "$ECR_REGISTRY/$ECR_REPOSITORY:latest"
```

Push the image to the private repository:

```bash
docker push "$ECR_REGISTRY/$ECR_REPOSITORY:latest"
```

Run the application locally for health validation:

```bash
docker run --rm -p 3000:3000 ecommerce-app:latest
```

## ECS Commands

List the cluster:

```bash
aws ecs describe-clusters \
  --clusters e-com-cluster \
  --region "$AWS_REGION"
```

Inspect the ECS service and its task counts:

```bash
aws ecs describe-services \
  --cluster e-com-cluster \
  --services e-com-task-service-javaihoy \
  --region "$AWS_REGION"
```

List tasks currently associated with the service:

```bash
aws ecs list-tasks \
  --cluster e-com-cluster \
  --service-name e-com-task-service-javaihoy \
  --desired-status RUNNING \
  --region "$AWS_REGION"
```

Inspect the task definition revision shown in the console:

```bash
aws ecs describe-task-definition \
  --task-definition e-com-task:2 \
  --region "$AWS_REGION"
```

## ECR Commands

Create the private repository if it does not already exist:

```bash
aws ecr create-repository \
  --repository-name e-com-app \
  --region "$AWS_REGION"
```

Inspect the pushed image:

```bash
aws ecr describe-images \
  --repository-name e-com-app \
  --image-ids imageTag=latest \
  --region "$AWS_REGION"
```

List repository images:

```bash
aws ecr list-images \
  --repository-name e-com-app \
  --region "$AWS_REGION"
```

## RDS Commands

The supplied evidence confirms PostgreSQL connectivity and SQL validation. Replace placeholders with the actual RDS endpoint and credentials; do not commit secrets.

Connect to the `shop` database:

```bash
psql \
  --host=<RDS-ENDPOINT> \
  --port=5432 \
  --username=appuser \
  --dbname=shop
```

Verify the product row count:

```sql
SELECT COUNT(*) FROM products;
```

Expected validation result from the supplied evidence:

```text
12
```

## Troubleshooting Commands

Inspect recent ECS service events:

```bash
aws ecs describe-services \
  --cluster e-com-cluster \
  --services e-com-task-service-javaihoy \
  --query 'services[0].events[:10]' \
  --region "$AWS_REGION"
```

Inspect a task that failed to start:

```bash
aws ecs describe-tasks \
  --cluster e-com-cluster \
  --tasks <task-arn> \
  --region "$AWS_REGION"
```

Review container logs when the task definition is configured with CloudWatch logging:

```bash
aws logs tail <log-group-name> \
  --since 30m \
  --follow \
  --region "$AWS_REGION"
```

## Validation Commands

Validate the local application health endpoint:

```bash
curl http://localhost:3000/health
```

Expected response shape:

```json
{
  "status": "ok",
  "database": "connected"
}
```

Validate an ALB-backed deployment when the DNS name is available:

```bash
curl http://<ALB-DNS-NAME>/health
```

Check the image digest and active status in ECR:

```bash
aws ecr describe-images \
  --repository-name e-com-app \
  --image-ids imageTag=latest \
  --query 'imageDetails[0].{tag:imageTags[0],digest:imageDigest,status:imageScanStatus.status,size:imageSizeInBytes}' \
  --region "$AWS_REGION"
```

Confirm ECS is maintaining two running tasks:

```bash
aws ecs describe-services \
  --cluster e-com-cluster \
  --services e-com-task-service-javaihoy \
  --query 'services[0].{desired:desiredCount,running:runningCount,pending:pendingCount,status:status}' \
  --region "$AWS_REGION"
```
