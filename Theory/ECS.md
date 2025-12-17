## ECS - Elastic Container Service

ECS is AWS’s container orchestration service.
It runs, scales, and manages Docker containers at scale.
Instead of you manually running docker run on EC2, ECS:
- pulls images (from ECR)
- schedules tasks (containers)
- restarts them if needed
- integrates with ALB, IAM, CloudWatch, etc.

#### Fargate (serverless compute for containers)
ECS has two main launch types:
1. EC2 launch type – Manage the EC2 instances
2. Fargate launch type – AWS manages the servers, you only specify CPU/memory

Using Fargate, means:
- No EC2 instance provisioning
- No SSH into nodes
- Just define task CPU, memory, container image, and AWS runs it

### Key Concepts
#### ECS Cluster
A logical group or environment where ECS tasks and services run.
Think of it like: “A folder / namespace for your containerized apps.”
For Fargate: Y
- You don’t see or manage EC2 nodes.
- The cluster is mostly a logical grouping + configuration context.

#### Task Definition
A Task Definition is like a blueprint or recipe for running container.
It includes:
- Which Docker image to use (ex: from ECR)
- CPU & memory reservations (ex: 0.25 vCPU, 512MB)
- Container port mappings (ex: container listens on 8000)
- Environment variables
- Logging config (CloudWatch Logs)
- IAM Task Role (permissions for the container)

Task Definition = “How should this app run?”

#### Task vs Service
Task
A single running unit created from a task definition.
- Like running docker run once
- It can start and stop
- if it dies, it doesn’t auto-restart (unless under a service)

Service
A long-running controller that:
- Ensures N copies (desired count) of a task stay running
- Works with Load Balancers
- Handles rolling updates

#### Questions
Q1: ECS vs Fargate vs EC2?
“ECS is the orchestration service. Fargate and EC2 are launch types. With EC2 launch type, I manage the instances. With Fargate, AWS manages the infrastructure and I only define tasks, which simplifies operations.”

Q2: What is a Task Definition in ECS?
“A Task Definition is a blueprint describing one or more containers — their image, CPU/memory, ports, environment variables, volumes, networking, and IAM roles. ECS uses it to know how to run tasks.”

Q3: How does ECS pull images from ECR?
“The Task Execution Role attached to the ECS task grants permissions to pull images from ECR. ECS uses this IAM role to authenticate and pull the specified image URI.”

Q4: What is an ECS Service?
“An ECS Service maintains a desired count of tasks from a task definition. It ensures high availability by restarting failed tasks and integrates with load balancers for incoming traffic.”

Q5: Why choose Fargate instead of EC2?
“Fargate eliminates the need to provision, scale, and patch EC2 instances. It’s ideal when I want to focus on containers and application logic instead of managing servers. It also offers more granular billing per vCPU/GB.”

Q6: How would you deploy a containerized app on ECS Fargate using ECR?
“I would push the Docker image to ECR, create a Task Definition referencing the ECR image, define CPU/memory and container port, then create an ECS Fargate service in a VPC, optionally attaching it to an ALB. The service will pull the image from ECR and keep the task running.”

Q7: What is the difference between ECR and ECS?
ECR and ECS solve two different problems in the container workflow. ECR is a container registry where it stores and versions Docker images securely using IAM.
ECS is a container orchestration service where it runs and manages containers, handles scaling, health checks, and integrates with load balancers.
In practice, I build a Docker image, push it to ECR, and then use ECS (often with Fargate) to pull that image and run it as a service.
ECR is for storage while ECS is for execution.
