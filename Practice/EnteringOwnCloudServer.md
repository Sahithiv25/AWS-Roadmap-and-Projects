### TASK: Create Key Pair Launch EC2 (Ubuntu) Open ports 22 (SSH), 80 (HTTP) SSH into EC2

#### What is this
A key pair is a secure login mechanism for EC2.
It contains:

- Public key → stored by AWS
- Private key (.pem file) → downloaded by you

You use the private key to SSH into your EC2 instance.
It replaces a password and is much more secure.

#### How to do this
- Go to EC2 in AWS console
- Left - Key Pairs
- Create key value pair
- Choose
-   Name: my-ec2-key
-   Key pair type: RSA
-   File format: .pem
- click create
- A .pem file downloads - keep it safe

#### Launch EC2 instance (Ubuntu)

Launching EC2 = starting your virtual machine in AWS.
You choose:
OS → Ubuntu
Instance type → t2.micro (free tier)
Security
Storage
This is your cloud server where you will later:
run Docker, deploy apps, run FastAPI

#### How to do this
- Go to EC2 dashboard
- Click Launch Instance
- Instance Name: ec2-learning-server
- Choose OS: Ubuntu Server 22.04 LTS
- Instance Type:t2.micro → free tier eligible
- Key Pair:select my-ec2-key you created earlier
- Network Settings:
    Create new security group
    Add inbound rules:
    SSH (22) → "My IP"
    HTTP (80) → "Anywhere (0.0.0.0/0)"
- Click Launch Instance

Your server is now running.

#### Open ports 22 and 80
Opening ports = configuring Security Group rules.
Security Groups are EC2’s firewalls.
Port 22 → required for SSH login
Port 80 → required to serve websites / HTTP traffic
Without these:
- You cannot connect to your EC2
- You cannot host anything

#### How to do this?
When launching EC2: Under Network Settings → Security Group
Add rules:
Rule 1: 
Type: SSH
Port: 22
Source: My IP
Rule 2:
Type: HTTP
Port: 80
Source: Anywhere (0.0.0.0/0)

If instance already exists:
Go to EC2 → Instances
Click your instance
Scroll to “Security” → Security Groups
Edit inbound rules

#### SSH into EC2
SSH is a secure way to log into your EC2 server terminal from your laptop.
It’s like sitting in front of your cloud computer.

Open your terminal on your laptop.
Navigate to where your .pem file is.
Run: chmod 400 my-ec2-key.pem

(this protects your key)
Then: ssh -i my-ec2-key.pem ubuntu@<your-public-ip>
You’ll get something like: ubuntu@ip-xxx-xx-xx-xx:~$

This means you are inside your AWS server.