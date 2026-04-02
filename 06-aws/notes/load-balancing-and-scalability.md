# Load Balancing and Scalability

### Keywords & Connections
- **Vertical scaling**: Scaling up a single EC2 instance in size (by increasing RAM/CPU), limited by the largest instance size available.
- **Horizontal scaling**: Dynamically increasing/decreasing amount of instances based on demand to handle incoming traffic.
- **Load balancer**: Distributes traffic across instances dynamically so that no single instance gets overloaded.
    - **Health check**: How load balancers check the state of an instance before redirecting traffic to it.
        - Health checks **sends a request to an instance**, for example to "port 4567, route /health". A response other than **200 OK** signal the load balancer to stop sending it traffic.
    - **Single endpoint**: load balancers provide single endpoint (**one url**) that **points to multiple instances** at a time, instead of having to type a different url for each instance.
    - **SSL termination**: When load balancer decrypts HTTPS requests and forwards it as plain HTTP request to the instance (reducing CPU needed by your instance)
- **ALB (Application load balancer)**: operates in layer 7 (OSI model), forwards data based on URL path, headers, query strings. Used for web applications and microservices.
- **NLB (Network load balancer)**: operates in layer 4, forwards TCP and UDP traffic at very low latency. Handles millions of requests per second, used for gaming and other real-time applications.
- **GWLB (Gateway load balancer)**: operates in layer 3, forwards data to firewalls and other security appliances.
- **CLB (Classic load balancer)**: old load balancer (not recommended by AWS), has no routing capabilities and therefore requires a load balancer on each service. 
- **ALB hostname vs. NLB static IP**:
    - ALB: uses DNS hostname that redirects to the ALB, since IP behind the scenes can change.
    - NLB: Has a fixed IP attached to it per AZ which never changes, one can also attach an elastic IP to it.
- **Port mapping**: Connecting a container to a specific port so traffic can reach it.
- **Target group**: grouping multiple targets of the same service for the purpose of managing and distributing traffic. Health checks are done at group level, only the individual unhealthy target stops receiving traffic, not the whole group.
    - 4 types of target groups: EC2 instances, ECS tasks, Lambda functions, or private IPs
- **X-Forwarded-For**: User IP's are put into HTTP header called "X-Forwarded-For" when forwarded to app/instance. Used because the ALB terminates the client's connection, so the EC2 instance only sees the ALB's private IP
- **High availability (HA)**:  Running your app across multiple AZs so it stays available if one AZ goes down
- **Auto scaling group (ASG)**: A service that keeps the right number of instances running at a time by scaling out (launching more instances when traffic increases) and scaling in (removing instances when traffic drops). 
    - ALB + ASG + Health Check trio: ASG starts instances (using AMI), ALB distributes traffic, health check detects a failure, ALB stops routing traffic to that instance, ASG removes the instance and launches a replacement.

### What problem does this solve?
- **Load balancers provide high availability (HA)** ensuring that your app stays available if one AZ goes down, while **ASG handles variable traffic** by scaling according to demand.
- **X-Forwarded-For**: Allows you to identify users IP for purposes such as rate limiting, geolocation, or security logging
- **ALB**: solves the problem of running multiple services using one LB by using target groups, instead of needing an LB for each service 

How does this connect to what I already know?
- SG referencing is used here: EC2 instances reference the ALB's SG ID in their inbound rules, meaning only traffic coming through the ALB is allowed
- Load balancer types (ALB, NLB) map to OSI layers from the Networking module


