## ALB - Application Load Balancer
- It distributes incoming traffic across multiple EC2 instances, containers, or Lambda functions.
- It's like A single public entry point (DNS name) that routes traffic to backend servers.
- Prevents server overload, downtime if 1 instance crashes and uneven traffic distribution.

#### Why use ALB
- Works at Layer 7 (HTTP/HTTPS)
- Can route based on path (/login, /api, /images)
- Can route based on hostnames
- Health checks (detects unhealthy instances)
- Highly scalable
- Get a single public DNS name

#### What is target group
A target group is a collection of backends (targets) that the ALB sends traffic to.

Targets can be: EC2 instances, ECS containers, Lambda functions, IP addresses

Think of a target group as: A list of servers behind the load balancer.

Why do we need it?
- Because the ALB doesn't send traffic directly to EC2 instances,
it sends traffic to target groups, which attach to instances.
- Also, target groups perform health checks. If health check fails ALB stops sending traffic to that instance

#### What is a listener
A listener is what tells the ALB: “Which port should I listen on, and where do I forward traffic?”

If someone visits your ALB DNS: http://<ALB-DNS-Name>
It receives the request on port 80, then forwards it to EC2 instance.

#### Access app via ALB DNS name
Every ALB has a DNS name like: my-alb-123456.us-east-1.elb.amazonaws.com

This is public URL.

ALB → Target Group → EC2 → Your App
You don’t need the EC2 public IP anymore, the load balancer handles everything.

Internet ----> ALB [DNS: my-alb.amazonaws.com]
                            |
                            |
                            V
                        Listener        
                    (port 80 rule)
                            |
                            |
                            V
                        Target Group
                        Health checks
                            |
                            |
                 --------------------
                 |                  |
                 |                  |
                 V                  V                       Healthy EC2 #1    Healthy EC2 #2 
            (serves traffic)        (serves traffic)
            

I set up an Application Load Balancer to distribute HTTP traffic across EC2 instances inside a public subnet. I created a target group with health checks, attached my EC2 instance to it, and configured a listener on port 80. After that, the ALB provided a DNS name that publicly routed traffic to my application. This enables fault tolerance, scaling, and high availability.                               
                