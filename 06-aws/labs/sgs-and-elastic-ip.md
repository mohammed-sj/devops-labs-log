# Lab: Security Groups & Elastic IPs

## Objective

Understand how Security Groups control traffic to EC2 instances, how Elastic IPs provide static public addresses, and how to distinguish between a timeout (SG issue) and a connection refused error (application issue).

---

## Lab 1 — Security Groups

### What I Did

1. Launched a t2.micro EC2 instance with a user data script that installed and started a simple Apache web server.
2. Confirmed the web server was reachable by navigating to the instance's public IP over HTTP (port 80).
3. Edited the instance's Security Group and **removed the HTTP inbound rule** (port 80).
4. Refreshed the browser, the page hung indefinitely (timeout). Traffic was being blocked before it ever reached the instance.
5. Re-added the HTTP inbound rule (port 80, source 0.0.0.0/0) and saved.
6. Refreshed again, the page loaded instantly.

### What I Learned

- Removing an inbound rule causes a **timeout**, not an error message. The traffic never reaches the instance because the SG blocks it at the network level.
- SGs are **stateful**: allowing inbound HTTP automatically allows the outbound response, no separate outbound rule needed.
- All inbound traffic is **blocked by default**. You only see what you explicitly allow.

---

## Lab 2 — Elastic IPs

### What I Did

1. Launched a new t2.micro instance with **Auto-assign public IP set to Disable** and no user data script.
2. Confirmed the instance had no public IPv4 address, it was unreachable from the internet.
3. Went to Elastic IPs tab in EC2 and **allocated a new Elastic IP** with default settings.
4. Associated the Elastic IP to the new instance.
5. Confirmed the instance now had a public IPv4 address (the Elastic IP).
6. Tried connecting to the IP in the browser, got **ERR_CONNECTION_REFUSED**.
7. This was expected: traffic reached the instance (SG allowed it), but there was no web server listening on port 80 since no user data script was added.

### Cleanup

- Disassociated the Elastic IP first, then released it. This order matters, an unattached Elastic IP incurs charges.
- Terminated both EC2 instances.

### What I Learned

- **Connection refused is not the same as timeout.** Connection refused means traffic reached the instance but nothing was listening. Timeout means traffic never got there.

