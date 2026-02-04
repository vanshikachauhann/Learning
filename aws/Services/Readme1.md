# VPC(Virtual Private Cloud)
An Amazon Virtual Private Cloud (VPC) is a logically isolated, private network dedicated to your AWS account, acting as a virtual data center in the cloud. It enables secure, customizable network environments to launch resources like EC2 instances, featuring user-defined IP address ranges, subnets, route tables, and network gateways. 
# Key Components and Features:
# Subnets:
A subnet is a smaller,segmented part of a large network that isolates and organizes devices within a specific IP address range.
# Route Tables: 
A Rout table is a set of rules called routes.That are used to determine where network traffic from your subnets or gateway is directed.Each Subnet in your VPC must be associated with a route table.
# Internet Gateway (IGW):
Enables communication between the VPC and the internet.
# NAT Gateway: 
Allows instances in private subnets to connect to the internet while preventing initiated inbound connections.
# Security: 
Uses Security Groups (instance-level firewall) and Network Access Control Lists (subnet-level firewall) to manage traffic.
# VPC Endpoints:
Enables private connection to AWS services (e.g., S3) without using an internet gateway.
# Peering/VPN: 
Allows connecting VPCs to each other or to on-premises data centers. 
# Bastion Host:
A special purpose instances that provides secure access to your instances in private subnets.
# ELastic IP Addresses:
static-IP Adresses designed for dynamic cloud computer.
# VPC Flow Logs:
Captures Informations about the IP traffic going to and from network interface in your VPC.
# Direct connect:
Establishes a dedicated network connection from your premissons to AWS.
# AWS clients VPN:
Managed VPN Services that enables secure remote access to AWS resoures and on permisses network using open VPN  based clients.


