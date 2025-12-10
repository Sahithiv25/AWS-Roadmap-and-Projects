## ECR - Elastic Container Registry
- ECR = AWS's private Docker image registry
- Its similar to docker hub, Github container registry and google container registry
- But its private, secure, integrated with AWS servies like ECS, EKS, lambda, fast image pulls inside AWS

#### Why do we need an ECR?
- A Docker image must live somewhere accessible for ECS or EC2 to pull it.
- You cannot deploy containers to ECS or EC2 directly from your laptop they require a registry.
- So ECR acts as the backend storage for your Docker images.
- Think of it like: “GitHub for Docker images.”
- Each repository in ECR contains: Multiple image versions (tags), 
Vulnerability scanning data, Push/pull permissions.

#### Questions
1. What is Amazon ECR?
Answer:
 ECR is AWS’s fully managed container registry used to store, manage, version, and scan Docker images. It integrates tightly with ECS, EKS, and EC2, allowing secure and high-performance pulling of container images within AWS. It replaces the need for external registries like Docker Hub in production environments.

2. Why use ECR instead of Docker Hub?
Answer:
I would choose ECR because it is private by default, has IAM-based authentication, integrates seamlessly with ECS/EKS deployments, supports VPC endpoints for private networking, and provides native vulnerability scanning. Docker Hub rate-limits anonymous pulls, while ECR provides reliable, scalable storage designed for AWS workloads.

3. How do you push a Docker image to ECR?
Answer:
The workflow is:
- Create an ECR repository.
- Authenticate Docker using an AWS CLI login command which generates a temporary token.
- Tag the image with the ECR repository URI.
- Push the image with docker push.
This uploads the Docker layers to ECR so they can be used by ECS or EKS.”

4. How does ECR authentication work?
Answer:
ECR uses AWS CLI to generate a short-lived authorization token. The docker login command uses this token to allow Docker to push or pull images. The token expires after 12 hours, ensuring security while eliminating the need for long-lived credentials.

5. Can ECR store multiple versions of an image? How?
Answer:
Yes. ECR supports image versioning through tags. Each push can use tags like latest, v1, v1.1, or Git commit hashes. This enables rollbacks, CI/CD integration, and environment-specific deployments.

6. What are ECR image scanning features?
Answer:
ECR offers two types of scanning:
- Basic scanning using the open-source Clair engine
- Enhanced scanning using Amazon Inspector
Both detect security vulnerabilities (CVEs) in container images and help enforce compliance and security policies.”

7. What’s the difference between Public ECR and Private ECR?
Answer:
Private ECR → for internal images, uses IAM authentication
Public ECR → hosts public images without Docker Hub rate limits
Public ECR provides higher throughput and no authentication needed for pulls.

8. How does ECS or EKS pull images from ECR?
Answer:
ECS tasks or EKS pods use an IAM role (task role or node role) that grants permission to pull images from ECR. The service retrieves a pull token automatically and fetches the layers securely, so no manual login is required.

9. How do you secure ECR repositories?
Answer:
I apply IAM policies to restrict who can push or pull images, enable encryption at rest (KMS), enforce image scanning, and optionally use VPC endpoints to keep traffic within the AWS network instead of the public internet.

10. What’s a typical CI/CD workflow with ECR?
Answer:
A pipeline builds a Docker image during the build stage, tags it with the ECR URI and commit hash, authenticates Docker to ECR, pushes the image, and updates the ECS service or EKS deployment. This fully automates container deployments.

11. Can ECR automatically clean up old images?
Answer:
Yes. ECR supports lifecycle policies that automatically remove untagged or old images to reduce storage cost and keep the registry clean.

12. What happens if two images have the same tag?
Answer:
The latest push overwrites the tag. Tags in ECR are mutable, so the same tag can point to a new image. This is why many teams also tag by Git commit SHA for immutability.

13. How do you pull an image from ECR to EC2?
Answer:
Authenticate Docker to ECR
Use docker pull <ecr-repo-url>:tag
If the EC2 instance has the right IAM permissions, this works without storing passwords.

14. What permissions are needed to push/pull ECR images?
Answer:
To push:
ecr:BatchCheckLayerAvailability
ecr:PutImage
ecr:UploadLayerPart
To pull:
ecr:BatchGetImage
ecr:GetDownloadUrlForLayer
This is often bundled into:
AmazonEC2ContainerRegistryFullAccess
AmazonEC2ContainerRegistryReadOnly

15. What is an ECR repository URI?
Answer:
It’s the address of the container repo, containing the account ID, region, and repository name.
Example:
123456789012.dkr.ecr.us-east-1.amazonaws.com/myapp:latest
You tag images using this URI to push to ECR.