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
- **Note:** Mentioned IP address is the Elastic IP address which is already created on GCP

## Create Virtual Private Gateway

![image](https://github.com/user-attachments/assets/14e9d01b-b66d-46b3-bff3-f6a1fa53c2c3)

- CLick on create Virtual Private Gateway
- Attach this Virtual Private Gateway with your VPC

## Create VPN Connection
- In Virtual Private Gateway field, select the gateway which you were created earlier named as aws-vpg
- In Customer Private Gateway field, select the gateway which you were created earlier named as aws-customergateway
- Static IP Prefix field = Enter the subnet of GCP on which your GCP instance is attached
- Local IPv4 network CIDR = 0.0.0.0/0 [It is the IPv4 range from GCP side]
- Remote IPv4 network CIDR = 0.0.0.0/0 [It is the IPv4 range from AWS side]

![image](https://github.com/user-attachments/assets/27f4ac58-37dd-4ada-a6a0-dddadf3c88eb)
![image](https://github.com/user-attachments/assets/9d44ce6b-5c7f-41e1-be1b-9187d9f00cc0)

- Click on create VPN Connection
- Once its state is available, select your VPN connection and click on Download Configuration.

![image](https://github.com/user-attachments/assets/8b865515-a8ed-4ad1-a9b4-6936ea5674f9)

- Select options as shown below and click on Download

![image](https://github.com/user-attachments/assets/4a627088-0e95-439d-bec3-6ed20132c550)

