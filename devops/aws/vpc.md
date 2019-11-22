# VPC

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
