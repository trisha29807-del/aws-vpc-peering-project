# AWS VPC Peering Project

> **Project:** Secure Communication Between Two Amazon VPCs Using VPC Peering  
> **Author:** Trisha · AWS Internship Batch 1  
> **AWS Region:** Asia Pacific (Sydney) — `ap-southeast-2`

## Overview

This project demonstrates private communication between two Amazon Virtual Private Clouds (VPCs) using VPC Peering, route tables, security groups, EC2 instances, and a bastion host. Validation included SSH access through the bastion, bidirectional ICMP tests, and a controlled security-group change to demonstrate failure and recovery.

## Architecture

### VPC A — `10.10.0.0/16`
- Public subnet: `10.10.1.0/24`
- Bastion host: `10.10.1.10`
- Private subnet: `10.10.2.0/24`
- Application A: `10.10.2.10`

### VPC B — `10.20.0.0/16`
- Private subnet: `10.20.1.0/24`
- Application B: `10.20.1.10`

The two VPCs use non-overlapping CIDR ranges. During the lab, VPC Peering and routes on both sides enabled private communication; security-group rules controlled permitted traffic.

## Test results

| Test | Result |
|---|---|
| SSH to private Application A through the bastion | Successful |
| SSH to private Application B through the bastion | Successful |
| App A (`10.10.2.10`) → App B (`10.20.1.10`) | 4/4 packets received; 0% loss |
| App B (`10.20.1.10`) → App A (`10.10.2.10`) | 4/4 packets received; 0% loss |
| Controlled ICMP rule removal | Ping failed: 4 sent, 0 received |
| ICMP permission restored | Connectivity restored |

**Limitation:** a pre-peering baseline failure was not captured. This is disclosed rather than presented as a completed test.

## Repository contents

- **[Project report (PDF)](docs/Trisha%20EWB%20VPC%20Peering%20Project%20(AWS%20Batch%201).pdf)** — the PDF currently present in the repository.
- **[Implementation and cleanup screenshots](screenshots/AWS_VPC_Peering_Evidence/)** — organized evidence folders.
- **[Project landing page source](index.html)** — static HTML page; it requires GitHub Pages to be enabled before it is available as a hosted website.

The editable DOCX and the separately named final PDF are **not currently in this repository**.

## Evidence index

The evidence directory currently contains 44 PNG screenshots, grouped as follows:

- [01 — Ping tests](screenshots/AWS_VPC_Peering_Evidence/01_Ping_Tests/)
- [02 — SSH access](screenshots/AWS_VPC_Peering_Evidence/02_SSH_Access/)
- [03 — VPC peering and routes](screenshots/AWS_VPC_Peering_Evidence/03_VPC_Peering_and_Routes/)
- [04 — Security groups](screenshots/AWS_VPC_Peering_Evidence/04_Security_Groups/)
- [05 — EC2 private IPs](screenshots/AWS_VPC_Peering_Evidence/05_EC2_Private_IPs/)
- [06 — Cleanup evidence](screenshots/AWS_VPC_Peering_Evidence/06_Cleanup/)

A copy of the currently uploaded PDF is also present inside the evidence directory; it is a report file, not a screenshot.

## AWS services and tools

- Amazon VPC and VPC Peering
- Amazon EC2
- Route tables and Internet Gateway
- Security Groups
- SSH / ProxyJump and ICMP
- Git and GitHub

## Key learning outcomes

- Configure VPCs and subnets with non-overlapping IPv4 CIDR ranges.
- Understand why both VPC route tables need routes to the peer CIDR.
- Use security groups to control reachability over a peering connection.
- Access private EC2 instances through a bastion host.
- Verify connectivity, troubleshoot a controlled failure, and record cleanup evidence.

## Cleanup and security

The cleanup evidence documents termination of the lab instances and removal of the lab networking resources. The final VPC screenshot shows both lab VPCs absent while one other VPC remains. AWS billing data can lag, so the Billing console should be checked separately.

Do not commit private keys (`.pem` files), passwords, access keys, tokens, or other credentials. Review screenshots for sensitive or unrelated account details before publishing them in a public repository.

## Author

Trisha · [GitHub profile](https://github.com/trisha29807-del) · [Repository](https://github.com/trisha29807-del/aws-vpc-peering-project)
