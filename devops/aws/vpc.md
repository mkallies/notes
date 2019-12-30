# VPC

tl;dr

CIDR: IP Range
VPC: Virtual Private Cloud -> define a list of IPv4 & IPv6 CIDR here
Subnets: Tied to an AZ, also define a CIDR block
Internet Gateway: at the VPC level, provides IPv4 & IPv6 internet access
Route Tables: must be edited to add routes from subnets to the IGW, VPC peering connections, VPC endpoints etc...
NAT Instances: deprecated, use NAT Gateway
NAT Gateway: managed by AWS, provides scalable internet access to private instances, IPv4 ONLY
Private DNS + Route 53: enable DNS resolution + DNS hostnames (VPC)
Network ACL: Stateless, subnet rules for inbound and outbound traffic, don't forget ephemeral ports
Security Groups: stateful, operate at the EC2 instance level

VPC Peering: connect 2 VPCs with non overlapping CIDR, non transitive
VPC Endpoints: Provide private access to AWS services (S3, DynamoDB, CloudFormation, SSM) within VPC
VPC Flow logs: Can be setup at the VPC / Subnet / ENI level, for ACCEPT and REJECT traffic, helps identifying attacks, analyze using Athena or CloudWatch Log insights

Bastion Host: public instance that you can SSH into, then SSH into instances that are in a private subnet
Site to Site VPN: setup a Customer Gateway on datacenter, a Virtual Private Gateway on VPC, and site-to-site VPN over public internet
Direct Connect: setup a VPG on VPC and establish a direct private connection to an AWS Direct Connect Location
Direct Connect Gateway: setup a DC to many VPC in different regions
Internet Gateway Egress Only: like a NAT gateway but for IPv6, only allows outgoing traffic -> like a private subnet


A default VPC:

- Created in each region when an AWS account is created
- Has default CIDR, security group, N ACL, and route table
- Has an internet gateway by default

It's best to name your subnets. This helps when you need to delete or edit a subnet

A custom VPC:

- Created by user
- User can decide on CIDR
- Has its own default security group, N ACL, route tables
- Does not have an internet gateway by default, must be created if needed

## CIDR (Classless Inter-Domain Routing) - IPv4

  - CIDR are used for Security groups rules or AWS networking in general
  - They help to define an IP address range
    - WW.XX.YY.ZZ/32 === one IP
    - 0.0.0.0/0 === all IPs
    - We can define our own -> 192.168.0.0/26 = 192.168.0.0 - 192.168.0.63 (64 IPs)
  - CIDR has two components
    - The base IP (xx.xx.xx.xx)
    - The subnet mmask (/26)
  - The base IP represents an IP contains in the range
  - The subnet mask defines how many bits can change in the IP

Subnet Masks

  - The subnet masks basically allows part of the underlying IP to get additional next values from the base IP

  - /32 allows for 1 IP = 2^0
  - /31 allows for 2 IP = 2^1
  - /30 allows for 4 IP = 2^2
  - ...
  - /0 allows for all IPs = 2^32

- /32 - no IP number can change (192.168.0.0)
- /24 - last IP number can change (192.168.0.x)
- /16 - last 2 places can change (192.168.x.x)
- /8 - last 3 places can change (192.x.x.x)
- /0 - all IP numbers can change

https://ipaddressguide.com/cidr


## Security groups

- Software firewall for an instance
- Stateful

Launching an EC2 instance

- Must always have a security group specified during its launch.
- Can create or use an existing one
- Can't delete a default security group
- SGs are VPC resources, meaning different ec2 instances in different availability zones, belonging to the same VPC can have the same security group applied to them

Default security group in a default or custom VPC will have:
- Inbound rules allowing instances assigned the same security group to talk to one another
- All outbound traffic is allowed

Custom security group:
- No inbound rules, must add rules
- All outbound traffic is allowed

## Network ACL (Access Control Lists)

- Allows access at the subnet level
- Stateless
- A subnet must be associated with a N. ACL, if you do not specify the NACL, the subnet will get associated
with the default NACL automatically
- Can create custom NACL
- default NACL allows all inbound and outbound traffic (not good for security!)
- custom NACL blocks all inbound and outbound traffic by default

## Network Address Translation (NAT)
- NAT instance is configured in a public subnet
- NAT instance needs to be assigned a security group
- NAT instance is there to enable the private subnet EC2 instances to get to the internet
- Public traffic can't access private subnet
- Can only access via SSH
- EC2 instances in the public subnet do not need to go through NAT to reach instances on the private subnet

## VPC Peering

- Is a connection between 2 VPcs that enables you to route traffic between them using private IPv4 or IPv6 address
- Can connect VPCs in different regions or same region
- Need to adjust route tables

## AWS Transit Gateway
