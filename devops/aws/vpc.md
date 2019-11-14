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
