## AWS Global Infrastructure

### Keywords & Connections
- **Regions** = Geographical locations from which AWS operates. Each contains multiple AZs. Chosen based on 4 factors: compliance, available services, latency, pricing
- **Availability Zones (AZs)** = Discrete data centers (or clusters) within a region, each with independent power and networking. Connected to each other via high-bandwidth, low-latency links. Typically 3–6 per region
- **Edge Locations** = 400+ CDN endpoints that cache content close to end users (part of CloudFront). Separate from the Region/AZ hierarchy
- **Region-scoped vs Global** = Most services (EC2, S3) exist only in the region you create them. Some (IAM, Route 53, CloudFront) are global

### What problem does this solve?
- Regions give you control over where infrastructure lives, this is critical for legal compliance and reducing latency
- AZs provide fault tolerance when you deploy across multiple AZs: each has independent power/networking, so if one fails, your application continues running in the others.
- Edge locations reduce latency by serving cached content from locations physically near end users

### My confusion / questions
- Initially confused Regions with AZs: the key distinction
  is that a Region is a geographic area, AZs are the actual
  infrastructure inside it
