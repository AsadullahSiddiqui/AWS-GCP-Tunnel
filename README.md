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

- View the details of downloaded files and save the details which are shown below, these details will use further in GCP
- As we created only 1 tunnel for traffic, thats why we only consider information of #IPSec Tunnel #1

![image](https://github.com/user-attachments/assets/4e90e5a3-a6c4-47aa-b3b8-a2aed6295e91)

## Enable Route Propagation
- Select your Public Route Table
- Click on Actions, select Edit Route Propagation
- Enable route propagation and save

**Everything is ready from AWS Side, now we will work on GCP**


## Steps on AWS
- Create 1 VPC with best practices with atleast 1 subnet [subnet=172.16.0.0/24]
- Create 1 VM in Compute Engine having Ubuntu OS.
- Create a Firewall Rules which allows ports[ssh, icmp]
- Reserve 1 External Static IP Address from VPC > IP Addresses
- External Static IP = 192.0.1.6

## Create VPN 
- Search Network Connectivity in GCP
- Select VPN and click on VPN, then press create VPN Connection
- Select Classic VPN

  ![image](https://github.com/user-attachments/assets/e6c5a225-c13f-4da6-834f-054e6af34a26)

- Click on Continue
- In Network field, select the VPC which you were created earlier.
- In region Field, select the region where you have created External Static IP.
- In IP Address field, 
