# EC2 Storage (EBS, AMI, EFS) 

### Keywords & Connections
**Network drive**: Storage that lives in a data center that is accessed through the internet.
**EBS (Elastic Block Store)**: A virtual network drive bound to a single AZ. Attached to one instance at a time to increase available disk space. The storage it provides is both persistent and detachable. Can be likened to a usb stick for your instance.
**EFS (Elastic file system)**: Similar to EBS except that it works across multiple AZs, this is to ensure high availability. Multiple EC2 instances can connect to it and edit its files simultaneously. Size is scalable, meaning it increases and decreases based on demand and that there's no need to provision size (as opposed to EBS where you choose size upfront). Downside is that it costs 3x what EBS does.
**AMI (Amazon Machine Image)**: A snapshot of an instance, used to save start up time of an instance. Auto-scaling groups (ASGs) use this to replace faulty instances with new ones.

### What problem does this solve?
- **EBS and EFS** provide persistent storage ensuring that data is saved on instance shutdowns.
- **AMIs** saves you time of not having to manually install and configure every new instance you start, and this is done automatically using **ASGs**.

### How does this connect to what I already know?
- **EBS** is like an external hard drive, except it’s a network-attached disk that provides persistent storage for a virtual server.
- **EFS** extends that idea to a shared folder that multiple computers can access, like a shared drive on a home network. 
- **AMI** is like making a backup of your computer in case you would like to restore it at a certain point.

