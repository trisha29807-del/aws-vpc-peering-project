# AWS VPC Peering Project

## Overview
This project demonstrates private communication between two Amazon Virtual Private Clouds (VPCs) using AWS VPC Peering, EC2 instances, route tables, security groups, and a bastion host.

## Objectives
- Create two separate VPCs with non-overlapping CIDR ranges.
- Configure public and private subnets.
- Establish a VPC peering connection.
- Configure routes for communication between the VPCs.
- Use a bastion host to access private EC2 instances through SSH.
- Verify connectivity using ICMP ping tests.
- Test security group rules by blocking and restoring ICMP traffic.

## Architecture

**VPC A — 10.10.0.0/16**
- Public subnet: 10.10.1.0/24
- Private subnet: 10.10.2.0/24
- Bastion host in the public subnet
- App-A EC2 instance in the private subnet

**VPC B — 10.20.0.0/16**
- Private subnet: 10.20.1.0/24
- App-B EC2 instance in the private subnet

The two VPCs are connected through a VPC peering connection. Route tables and security groups control the permitted traffic.

## Implementation
1. Created both VPCs and their subnets.
2. Configured an Internet Gateway for public access to the bastion host.
3. Launched the bastion, App-A, and App-B EC2 instances.
4. Established and activated the VPC peering connection.
5. Added the required routes to the route tables.
6. Configured security groups for SSH and ICMP traffic.
7. Connected to private instances through the bastion host.
8. Tested connectivity and verified the effect of changing security group rules.

## Testing and Results
- SSH access to the private EC2 instances through the bastion host was verified.
- Ping from App-A to App-B succeeded after routing and security rules were configured.
- Reverse ping from App-B to App-A also succeeded.
- A controlled ICMP security group change caused ping traffic to fail.
- Restoring the ICMP rule restored connectivity.

## Technologies Used
- Amazon Web Services (AWS)
- Amazon VPC and VPC Peering
- Amazon EC2
- Route Tables and Internet Gateway
- Security Groups
- SSH and ICMP
- GitHub

## Evidence
Screenshots of the AWS configuration, routing, security group rules, SSH access, connectivity tests, and cleanup will be added to this repository.

## Learning Outcomes
This project provided practical experience with VPC networking, private IP communication, routing, network security, bastion-host access, and connectivity troubleshooting.

## Security Note
Private keys, passwords, access tokens, and other credentials must never be uploaded to this repository.
