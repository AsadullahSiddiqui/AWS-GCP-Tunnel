# AWS-GCP-Tunnel
Establish secure connectivity between AWS and GCP instances using a VPN tunnel.

## Overview
- **Platform:** AWS and Google Cloud
- **Purpose:** Establish secure connectivity between AWS and GCP instances using a VPN tunnel.

## Prerequisites
- AWS and GCP accounts with sufficient permissions.
- The Private IP network of GCP and AWS must be different, otherwise it will overlap and connection will not estalish.

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


## Steps on GCP
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
- In IP Address field, enter the External Static IP = 192.0.1.6

 ![image](https://github.com/user-attachments/assets/1848c65e-cdc1-4f5a-acd5-0984289a5a1b)

- We will create only 1 tunnel here, details of tunnels are mentioned below
- In Remote Peer IP Address, enter the Outside IP of AWS, which you can check in AWS VPN Configuration file, as shown above
- In IKE version field, select IKEv1 as you selected in AWS.
- In IKE pre-shared Key field, enter the pre-shared key, whcih you can find in AWS VPN Connection Configuration file

![image](https://github.com/user-attachments/assets/afe39f5e-007a-4615-a7ae-c6b090ed3c74)

- In Routing Option, select Route-based
- In Remote Network IP Ranges, select the subnet of AWS on which your EC2 instance is running.
- press done

![image](https://github.com/user-attachments/assets/1da0d06c-feca-4316-ab9b-18b831bc4d14)

- Click on Create
- Your VPN connection from AWS to GCP has established

## Test your VPN connection

- Access your AWS EC2 instance, and execute **ping (IP address of GCP Instance)**
- It will communicate successfully with GCP VM.
- Now, SSH your Google VM instance, and execute **ping (IP address of EC2 Instance)**
- It will communicate successfully with AWS EC2 Instance

## Some Use Cases

- **Disaster Recovery and Failover:** You can set up AWS and GCP instances as backups for each other, providing high availability. In case one cloud provider experiences downtime, you can failover to the other to ensure continuous operation.
- **Data Backup and Storage:** This connection allows you to securely transfer backups from AWS to GCP or vice versa, distributing data storage across multiple clouds and leveraging each provider's storage solutions for redundancy.
- **Cross-Cloud Applications:** For applications that require specific services from each cloud, a secure connection enables AWS and GCP resources to work together seamlessly. For instance, an app might leverage AI services from GCP while hosting its core infrastructure on AWS.


## Conclusion
This project establishes a secure link between an AWS EC2 instance and a GCP VM instance to enable multi-cloud operations. This setup provides resilience, allowing for disaster recovery, load balancing, and cross-cloud data processing. It also supports data synchronization, backup solutions, and hybrid cloud security. The connection enhances DevOps capabilities, enabling testing and deployment pipelines across both clouds. This project empowers flexibility by leveraging the unique strengths of AWS and GCP for a versatile, high-performance multi-cloud environment.
