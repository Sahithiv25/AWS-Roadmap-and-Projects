## TASK
1️⃣ Draw your own VPC diagram
2️⃣ Create a new VPC manually
3️⃣ Add 1 public + 1 private subnet

#### Draw your VPC Diagram
![alt text](images/VPC_diagram.png)

#### Create a new VPC mannually
Go to: AWS Console → VPC → Your VPCs → Create VPC
Choose VPC Only (Manual Setup)
| Field           | Value          |
| --------------- | -------------- |
| Name tag        | `learning-vpc` |
| IPv4 CIDR block | `10.0.0.0/16`  |
| IPv6            | None           |
| Tenancy         | Default        |
Click create VPC

#### Add a public subnet
Now we add the first subnet
Go to: VPC dashboard -> subnets -> create subnet
| Field           | Value                         |
| --------------- | ----------------------------- |
| VPC             | `learning-vpc`                |
| Subnet name     | `public-subnet-1`             |
| AZ              | Choose `us-east-1a` (any one) |
| IPv4 CIDR block | `10.0.1.0/24`                 |
Click create subnet

A subnet becomes public only if its route table sends traffic to the Internet Gateway.

But first, we must create an IGW.

#### Create an internet gateway
Go to: VPC→ Internet Gateways → Create internet gateway
Click create
Now attach it:
Click the IGW
Choose Actions → Attach to VPC
Select learning-vpc
VPC now has internet capability.

#### Create a public route table
Go to: Route Tables → Create Route Table
| Field | Value          |
| ----- | -------------- |
| Name  | `public-rt`    |
| VPC   | `learning-vpc` |
Click create
Now edit routes:
Select public-rt
Click Routes → Edit routes
Add:
Destination: 0.0.0.0/0
Target: Internet Gateway (select learning-igw)

Associate the route table with the public subnet:
- In the same route table
- Go to Subnet associations
- Click Edit subnet associations
- Select public-subnet-1
- Save

Public subnet is officially public

To launch an EC2 inside the public subnet: go to EC2 and create
instance. In network settings give the details of VPC and public subnet. Ensure security group allows SSH. Access it via SSH.