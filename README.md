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
