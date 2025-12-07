## EC2 - Elastic Cloud Compute

#### One line definition
EC2 is AWS’s service that gives you virtual machines in the cloud that you can fully control like CPU, memory, storage, OS, networking, security and pay only for what you use.

#### EC2 = A computer in AWS’s data center
Instead of buying your own hardware, AWS gives you:
- a virtual computer
- where you choose the specifications
- and it runs on Amazon’s physical servers
You can SSH into it like your laptop, install software, run servers, deploy apps, etc.

Why it’s important
When companies say “We deployed our backend to AWS”, most of the time, it’s running on EC2 or an EC2-based service.

#### What EC2 lets you control
| Component           | Your Control                       |
| ------------------- | ---------------------------------- |
| **Instance Type**   | CPU + RAM (ex: t2.micro, m5.large) |
| **AMI**             | OS (Ubuntu, Amazon Linux, Windows) |
| **Storage**         | Disk type, size (EBS volume)       |
| **Networking**      | VPC, subnets, secure access        |
| **Security Groups** | Open ports (firewall)              |
| **Key Pair**        | SSH access                         |

#### Why companies use EC2
✔ Flexibility
✔ Scalability
✔ Pay-as-you-go
✔ Highly reliable hardware

EC2 provides resizable compute capacity in the cloud. It allows you to create and manage virtual servers with full control over OS, networking, storage, and security. It’s used to host applications, APIs, databases, or any workload that needs a server.


