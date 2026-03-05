## IAM fundamentals

### Keywords & Connections
- Permissions can be given to individual users as well as groups. Users can be part of multiple groups and gain permissions from each group, whilst also having specific permissions given to them (inline policies)
- Least privilege principle is to give users only as much permissions as they need to do their job
- Root account has unrestricted access to everything, while IAM users are given specific permissions through policies. Best practice: lock away root account away and use IAM users for daily work.  
- Policies are json documents defining who can do what. Key parts: Effect (allow/deny), Action (what they can do), Resource (which specific AWS object)
- MFA adds a second layer of security beyond passwords. Should be enabled on root and all IAM users.

### What problem does this solve?
- Operating through IAM users and applying least privilege principle reduces the blast radius if someone makes a mistake or an account gets compromised.
- Giving permissions to groups makes it easier to organize and manage roles, instead of having to give each individual user their permissions
- Policies gives you a lot of control over exactly what actions are allowed on which resources.

### How does this connect to what I already know?
Linux permissions use `chmod` with u/g/o to control who can read/write/execute files. IAM does the same for cloud resources; policies are like permission rules, groups work like Linux groups, and the root account is like the Linux root user.
