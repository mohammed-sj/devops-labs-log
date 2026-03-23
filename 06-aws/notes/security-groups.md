## Security Groups & IP Addressing

### Keywords & Connections
- **Security Groups (SGs):** Virtual firewalls that sit outside an EC2 instance, filtering which traffic is allowed in and out.
- **Stateful:** If an inbound connection is allowed, the outbound response is automatically allowed too.
- **Allow-only:** SGs only have allow rules, no deny rules. Anything not explicitly allowed is denied by default. Rules can be set for both inbound and outbound traffic.
- Each SG rule requires a port, protocol, and IP range.
- **SG referencing:** Instead of hardcoding IPs, you allow traffic from any instance wearing a specific SG badge. Useful when instances are created/destroyed dynamically (e.g. auto-scaling).
- **IPv4:** Supports both private and public IPs. Public IPs are globally unique; private IPs only need to be unique within their network. ~4.3 billion addresses exist but are running out, driving the adoption of IPv6.
    - Private IPv4 ranges: 10.0.0.0, 172.16.0.0–172.31.x.x, 192.168.0.0
- **IPv6:** Public only in AWS (no private range). Far larger address space than IPv4.
- **Elastic IP:** A static public IPv4 you own. Stays the same across instance stop/starts, unlike regular public IPs which change dynamically.
- **Common ports:** SSH = 22, HTTP = 80, HTTPS = 443, RDP = 3389, PostgreSQL = 5432
- **Debugging rule:** Timeout = SG issue. Connection refused = app issue.

### What problem does this solve?
Security Groups keep EC2 instances secure by letting you control exactly which traffic can reach your instance and which cannot.

### How does this connect to what I already know
- Ports and protocols (TCP/UDP) was mentioned in the Networking module, SGs are the AWS implementation of firewall rules applied to those same ports.
- Private vs public IPs connect to how NAT works: a router translates private IPs to public ones, same concept as an internet gateway in AWS.

Quick Example
Removed the HTTP inbound rule (port 80) from my instance's SG resulted in browser timed out. Re-added it, page loaded instantly. Also tested accessing an instance with no web server installed: got "connection refused" instead of a timeout. Timeout = SG blocking traffic. Connection refused = traffic got through but nothing is listening. Full lab write-up in 06-aws/labs/
