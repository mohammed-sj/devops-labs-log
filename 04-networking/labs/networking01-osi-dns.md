# *2025-11-26* — Networking: OSI Model & DNS

## OSI Model

The OSI model is just a way to describe how data travels across a network.  
Brief explanation of each layer:

1. **Physical:** Where data moves as signals through electricity (copper cables), light (fiber), or radio waves (WiFi).
2. **Data Link:** The LAN layer where devices talk using MAC addresses and frames.
3. **Network:** The layer where routers pick the path for data to travel across different networks using IP addresses.
4. **Transport:** The layer that breaks data into pieces and decides how it's delivered (TCP for safe, UDP for fast).
5. **Session:** Starts, maintains, and ends the connection between two devices.
6. **Presentation:** Encrypts, compresses, and formats data so it's readable.
7. **Application:** Where users and apps actually interact with the network.

---

## DNS

DNS is the system that turns domain names into IP addresses.  
Brief explanation of main components:

- **Recursive resolver:** The server my device asks first. It checks its cache and, if needed, goes out and finds the answer from other DNS servers.
- **Authoritative nameserver:** The server that holds the real DNS records for a domain — the source of truth.
- **Zone file:** A text file on an authoritative server that stores all DNS records for a domain.
- **Resource record:** A single DNS entry that describes something about a domain (like an IP, alias, mail server, or text value).
- **/etc/hosts:** A local override file on my machine, anything written here is used before DNS.

---

## Cheatsheet

- `nslookup example.com` | simple DNS query tool that shows basic records  
- `dig example.com` | detailed DNS lookup (add +short to only show the IP)  
- `dig NS example.com` | shows the authoritative nameservers for a domain

---

## Why This Matters
Understanding the OSI model helps me see where in the path things can break and makes troubleshooting feel more structured.DNS concepts matter because almost every connection or outage touches DNS in one way or another, so knowing the basics is essential.

