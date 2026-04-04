# Auto Scaling groups

### Keywords & Connections

- **ASG (Auto Scaling groups)**: an AWS service that scales amount of instances based on demand (it's free, you only pay for the instances)
    - **Three capacity settings**: can be configured to keep within minimum, desired and max amount of instances.
    - **Launch template**: the "recipe" ASG use to start new instances, includes AMI, instance type, SGs, key pair, user data, VPC/subnets, LB to register with.
    - **Three scaling policy types**:
        - **Target tracking**: set a desired threshold (like CPU usage of 40%), ASG will automatically add or remove instances to keep the metric at this target. 
        - **Step scaling**: you define how much you want to scale at specific thresholds.
        - **Scheduled scaling**: set the scaling at a specific time period
- **CloudWatch**: monitors custom metrics to signal the ASG when to scale out/in.
- **ALB + ASG lifecycle**:
    - 1. ALB detects unhealthy instance via health check
    - 2. ALB stops routing traffic to it
    - 3. ASG notices the instance is unhealthy, terminates it, and launches a replacement using the launch template
    - 4. New instance registers with ALB, passes health check, receives traffic    

### What problem does this solve?
- **ASG** scaling helps in **reducing unnecesary costs** by avoiding over provisioning, while simultaneously **keeping your app from crashing** by avoiding under provisioning.
    - With services like CloudWatch and configurations on launch template and scaling policies, this scaling process can become fined tuned

### How does this connect to what I already know?
- AMIs are chosen within the Launch template
- Connection draining kicks in during a scale in event 
