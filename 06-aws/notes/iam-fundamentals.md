## IAM fundamentals

### Keywords & Connections
* Permissions can be given to individual users as well as groups. Users can be part of multiple groups and gain permissions from each group, whilst also having specific permissions given to them (inline policies)
* Least privilege principle is to give users only as much permissions as they need to do their job
* Root account has unrestricted access to everything, while IAM users are given specific permissions through policies. Best practice: lock away root account away and use IAM users for daily work.
* Policies are json documents defining who can do what. 
   * Key parts: Effect (allow/deny), Action (what they can do), Resource (which specific AWS object)
* MFA adds a second layer of security beyond passwords. Should be enabled on root and all IAM users.
* IAM Roles - temporary roles with permissions attached to services. Unlike users, roles have no permanent credentials.  
* Three ways of accessing AWS:
   * AWS management console:
      * Webb-based interface
      * Click based operations (click-ops)
      * Accessed through username, password and MFA
   * CLI (command line interface)
      * Tool that lets you interact with AWS services from the terminal
      * Faster than the console and useful for automation and scripting
      * Authenticated using access key
   * SDK (Software development kit)
      * Libraries used by developers to interact with AWS services through code
      * Used inside applications
      * Communicates with AWS through APIs
      * Can use access keys or other credential methods
* Credential reports - Gives you an overview of users and the status of their credentials: if their MFA is setup, last time they changed passwords, access keys and last time they were rotated etc. 
* Access advisor - A tool for applying least privielege principle by showing which services users have permission to access and when they were last accessed.

### What problem does this solve?
* Operating through IAM users and applying least privilege principle reduces the blast radius if someone makes a mistake or an account gets compromised.
* Giving permissions to groups makes it easier to organize and manage roles, instead of having to give each individual user their permissions
* Policies gives you a lot of control over exactly what actions are allowed on which resources.
* Examples for why services need roles:
   * EC2 - to access S3 and databases    
   * Lambda - to process files and write logs    
   * CloudFormation - to build infrastructure    
   * CI/CD - to deploy application
### How does this connect to what I already know?
Linux permissions use chmod with u/g/o to control who can read/write/execute files. IAM does the same for cloud resources; policies are like permission rules, groups work like Linux groups, and the root account is like the Linux root user.


