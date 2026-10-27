# AWS VPC Peering Project

> **Project:** Secure Communication Between Two Amazon VPCs Using VPC Peering  
> **Author:** Trisha · AWS Internship Batch 1  
> **Region:** Asia Pacific (Sydney) — `ap-southeast-2`

## Overview

This project demonstrates private communication between two Amazon Virtual Private Clouds (VPCs) using VPC Peering, EC2 instances, route tables, security groups, and a bastion host. The implementation was tested with SSH and ICMP connectivity checks, including a controlled security-group change to observe failure and recovery.

## Architecture

**VPC A — `10.10.0.0/16`**
- Public subnet: `10.10.1.0/24` — bastion host (`10.10.1.10`)
- Private subnet: `10.10.2.0/24` — Application A (`10.10.2.10`)

**VPC B — `10.20.0.0/16`**
- Private subnet: `10.20.1.0/24` — Application B (`10.20.1.10`)

The VPCs were connected by a peering connection during testing. Routes and security groups controlled permitted traffic. The AWS resources used for the lab were removed after testing; the final VPC screenshot shows both lab VPCs absent and one other VPC remaining.

## Objectives

- Configure two VPCs with non-overlapping CIDR ranges.
- Create public and private subnets and configure route tables.
- Establish VPC peering and allow the required traffic.
- Access private EC2 instances through a bastion host using SSH ProxyJump.
- Verify connectivity in both directions using ICMP ping.
- Demonstrate the effect of a security-group rule change.
- Capture implementation and cleanup evidence.

## Implementation and test results

- SSH access to both private EC2 instances through the bastion host succeeded.
- App A `10.10.2.10` → App B `10.20.1.10`: 4 packets received, 0% loss.
- App B `10.20.1.10` → App A `10.10.2.10`: 4 packets received, 0% loss.
- Temporarily removing the relevant inbound ICMP permission caused the ping to fail (4 sent, 0 received); restoring the rule restored connectivity.
- **Limitation:** a pre-peering baseline failure was not captured and is disclosed in the report.

## Project documents

Once uploaded, the files will be available here:

- [Final project report (PDF)](docs/Trisha_EWB_VPC_Peering_Final.pdf)
- [Editable project report (DOCX)](docs/Trisha_EWB_VPC_Peering_Updated.docx)
- [Implementation and cleanup screenshots](screenshots/)

## Evidence structure

Screenshots should be organized as follows:

- `screenshots/01_Ping_Tests/`
- `screenshots/02_SSH_Access/`
- `screenshots/03_VPC_Peering_and_Routes/`
- `screenshots/04_Security_Groups/`
- `screenshots/05_EC2_Private_IPs/`
- `screenshots/06_Cleanup/`

## AWS services and tools

- Amazon VPC and VPC Peering
- Amazon EC2
- Route tables and Internet Gateway
- Security Groups
- SSH / ProxyJump and ICMP
- GitHub

## Key learning outcomes

- How routes on both sides are required for private VPC-to-VPC connectivity.
- How security groups affect reachability even when peering is active.
- How to reach private instances through a bastion host.
- How to validate connectivity, troubleshoot a controlled failure, and document cleanup.

## Security and cleanup notes

- Never commit private keys, passwords, access tokens, or other credentials.
- Public repository screenshots should be checked for account identifiers and unrelated resources before uploading.
- Lab cleanup was performed after evidence capture. AWS billing data can lag; check the Billing console separately if needed.

## Author

Trisha — [GitHub profile](https://github.com/trisha29807-del)
