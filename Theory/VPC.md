## VPC - Virtual Private Cloud
VPC (Virtual Private Cloud) is own private network inside AWS where you place and control your cloud resources like EC2, RDS, and Lambda with complete control over IP addresses, subnets, routing, and security.

#### Why Do We Need a VPC?
Because AWS is shared infrastructure.
A VPC gives:
✔ A private address space
✔ Control over networking
✔ Separation between public and private resources
✔ Security boundaries
Every serious company uses VPCs to isolate workloads and enforce security.

#### VPC = Your private network
When you create a VPC, you assign it a CIDR block (IP range):
Example: 10.0.0.0/16

This gives 65,536 private IPs you can use. (2^16)
Inside this VPC, you create multiple subnets.

#### Subnets
A subnet is a slice of the VPC IP range.
Example VPC: 10.0.0.0/16

Example subnets:
10.0.1.0/24  → public subnet
10.0.2.0/24  → private subnet

Each subnet exists in one Availability Zone (AZ).

“A subnet divides the VPC into smaller networks. Public subnets allow internet-facing resources, private subnets host internal resources.”

#### Route Tables
Route tables determine where traffic goes from each subnet.
Each subnet must be associated with exactly one route table.
Example public route table:
Destination: 0.0.0.0/0
Target: Internet Gateway (igw-123)
Example private route table:
Destination: 0.0.0.0/0
Target: NAT Gateway (nat-123)
Route tables contain rules that define how traffic is routed within the VPC and to the internet.

#### Internet Gateway (IGW)
An Internet Gateway connects your VPC to the public internet.
You need an IGW if you want:
- EC2 to be accessible from the internet
- Static website hosting in public subnets
- Public IP addresses to work

“An Internet Gateway provides outbound and inbound internet access for resources in public subnets.”

#### NAT Gateway (Network Address Translation)
A NAT Gateway lets private subnets access the internet without exposing them publicly.
Use case:
- EC2 in private subnet needs to download updates
- RDS wants to reach out to AWS services
- Internal backend calls
Private instances → NAT Gateway → Internet
BUT inbound traffic cannot reach them.

“A NAT Gateway allows instances in private subnets to access the internet for outbound traffic while staying unreachable from the outside.”

#### Public vs Private subnets
Public Subnet:
Has a route to the Internet Gateway.
0.0.0.0/0 → IGW
Resources inside public subnets can:
- Have public IPs
- Be reached from the internet

Used for:
- Load balancers
- Bastion hosts
- Public-facing web servers

Private Subnet
Has a route to a NAT Gateway, not the internet gateway.
0.0.0.0/0 → NAT Gateway
Resources inside private subnets:
- Cannot be accessed from internet
- Can make outbound internet calls (through NAT)

Used for:
- Databases (RDS)
- Internal backend services
- Sensitive workloads

“Public subnets route to the Internet Gateway; private subnets route to a NAT Gateway.

#### Security Groups vs NACLs
Security Groups (SG):
Act as virtual firewalls for EC2 instances
Stateful: If inbound is allowed, outbound response is automatically allowed
Applied at the instance level
Only allow rules (never deny)

Example:
Allow inbound: port 22 from 1.2.3.4
Allow inbound: port 80 from anywhere

“Security groups are stateful firewalls attached to instances that define allowed inbound and outbound traffic.”

Network ACLs (NACLs):
Act as firewalls at the subnet level
Stateless: Every inbound rule needs a matching outbound rule
Have allow & deny rules
Rarely modified in practice

Example:
Allow inbound 80 from anywhere
Deny inbound 22 from anywhere

“NACLs are stateless firewalls at the subnet level that can explicitly allow or deny traffic.”

#### How everything works together
VPC (10.0.0.0/16)
│
├── Public Subnet (10.0.1.0/24)
│   ├── Route table → Internet Gateway
│   └── EC2 instance with public IP
│
├── Private Subnet (10.0.2.0/24)
│   ├── Route table → NAT Gateway → Internet Gateway
│   └── RDS/Backend servers (no public IP)
│
└── Security Groups + NACLs control traffic

#### Questions
Q1: What is the difference between public and private subnets?

“Public subnets route to the Internet Gateway, private subnets route to a NAT gateway. Public resources can be externally accessed; private ones cannot.”

Q2: SG vs NACL?

“Security groups are stateful and attach to instances. NACLs are stateless, attach to subnets, and support deny rules.”

Q3: Why use NAT Gateway?

“To allow private instances to make outbound internet calls without being publicly reachable.”

Q4: Why do we need route tables?

“Route tables define where traffic goes — to the internet gateway, NAT gateway, or internal subnets.”

Q5: Why create multiple subnets?

“For separation of public and private layers, high availability across AZs, and better security control.”