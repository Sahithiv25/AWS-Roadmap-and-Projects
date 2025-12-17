## TASK - AWS CLI commands

1. aws configure - configure AWS CLI sets access key, secret key, region
2. aws sts get-caller-identity - verify identify returns Account ID and IAM user/role
3. aws configure --profile dev
    aws s3 ls --profile dev - switch profiles

#### S3 commands
1. List buckets - aws s3 ls
2. list objects in a bucket - aws s3 ls s3://my-bucket
3. upload a file - aws s3 cp file.txt s3://my-bucket
4. download a file - aws s3 cp s3://my-bucket/file.txt
5. sync folder - swa s3 sync ./data s3://my-bucket/data (sync contents of local directory to S3 buckets)(used to upload datasets or static files)
6. delete objects - aws s3 rm s3://my-bucket/file.txt

#### EC2 commands
1. List instances - aws ec2 describe-instances
2. start/stop EC2 - aws ec2 stop-instances --instance-ids i-123; to start - aws ec2 start-instances --instance-ids i-123
3. list security groups - aws ec2 describe-security-groups

#### Cloudwatch commands
1. view logs for lambda/ECS - aws logs describe-log-groups
2. get log events - aws logs get-log-events/ --log-group-name /aws/lambda/my-func --log-stream-name stream-name
3. list metrics - aws cloudwatch list-metrics

#### ECR & ECS container commands
1. authenticate docker with ECR - aws ecr get-login-password --region region-name docker login --username name --password-stdin 
2. list ECR repositiories - aws ecr describe-repositories
3. list images in repo - aws ecr list-images --repository-name myapp
4. ECS list clusters - aws ecs list-clusters
5. list services in a cluster - aws ecs list-services --cluster my-cluster

#### Lambda API gateway
1. invoke lambda from cli - aws lambda invoke --function-name my-func response.json
2. list functions - aws lambda list-functions
3. view lambda logs - aws logs tail /aws/lambda/my-function --follow
4. list api gateway apis - aws apigateway get-rest-apis

