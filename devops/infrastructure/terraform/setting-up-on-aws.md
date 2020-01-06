# Setting up on AWS

0. Create an s3 bucket for the terraform state

1. Create VPC
1. Create public + private subnets

- Pass in VPC ID

3. Create security group

- Pass in VPC ID

4. Create internet gateway

- Pass in VPC ID

5. Create route table

- Pass in VPC ID

6. Create aws route

- Pass in route table's id
- Needs destination cidr block
- Pass in gateway id

7. Associate route table with subnets

- Pass in subnet ID
- Pass in route table ID
