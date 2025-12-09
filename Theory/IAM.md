## IAM - Identity and Access Management

IAM manages who (users/roles) can access what (resources) in AWS, and what actions they are allowed to perform.

IAM = permissions system of AWS.
Everything in AWS like EC2, S3, Lambda, RDS require permission.
IAM controls three things:
- Identity — who/what is accessing AWS
- Authentication — how they log in (passwords, access keys)
- Authorization — what they can/can’t do

#### IAM Users
Humans
Used for: developers, admins, DevOps engineers.
Authentication:
- username + password
- access keys (for CLI access)

Interview Answer: IAM users are for people who need long-term access to AWS.

#### IAM Roles
Machines
Roles are used by: EC2 instances, Lambda functions, ECS tasks, Applications
Roles provide temporary, automatically rotated credentials.

Example:
A Lambda function needs to read from S3 → attach AmazonS3ReadOnlyAccess role.

Interview Answer: IAM roles are assigned to AWS services or applications and provide temporary security credentials, making them safer for machine-to-machine access.

#### IAM Policies
JSON documents that say Allow or Deny actions on AWS resources.
- Example policy:
{
  "Effect": "Allow",
  "Action": ["s3:PutObject"],
  "Resource": ["arn:aws:s3:::my-bucket/*"]
}

Interview Answer: IAM policies define permissions in AWS. They specify which actions are allowed or denied on which resources.

#### Security Groups
Firewalls for EC2.
They control:
- inbound traffic (who can access your server)
- outbound traffic (what your server can access)

Example:
Allow SSH (port 22) only for your IP
Allow HTTP (port 80) for everyone

Interview Answer: Security groups are virtual firewalls for EC2 instances. They control incoming and outgoing network traffic using rules.

#### How EC2 + IAM + Security Groups work together
When you launch an EC2 instance:
- IAM decides who can launch or manage it
- Security group decides what traffic can reach the instance
- EC2 is the actual machine running your application