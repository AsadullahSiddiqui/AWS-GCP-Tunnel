# AWS-GCP-Tunnel
Establish secure connectivity between AWS and GCP instances using a VPN tunnel.

## Overview
- **Platform:** AWS and Google Cloud
- **Purpose:** Establish secure connectivity between AWS and GCP instances using a VPN tunnel.

## Steps on AWS

- Create 1 VPC with best practices[CIDR=10.0.0.0/16]
- Create 1 EC2 Instance having Ubuntu OS.
- Create a Security Group which allows ports[ssh, icmp]

## Create Customer Gateway
![image](https://github.com/user-attachments/assets/e7503c57-8d52-40c7-a8c0-8ef779ec2bb6)

- CLick on create Customer Gateway
**Note:** Mentioned IP address is the Elastic IP address which is already created on GCP

## Create Virtual Private Gateway

![image](https://github.com/user-attachments/assets/14e9d01b-b66d-46b3-bff3-f6a1fa53c2c3)

- CLick on create Virtual Private Gateway
- Attach this Virtual Private Gateway with your VPC
