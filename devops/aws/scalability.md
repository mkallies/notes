# Scalability

## Types

Vertical scalability
Increasing the size of an instance

Horizontal scalability
Increase instance count

## High Availability

Running application in different availability regions

## Load balancing

User connects to load balancer, load balancer forwards to different instances
- Handles failures of instances by using health checks and rerouting to healthy instances
- It costs less to setup my own load balancer but it will be a lot more effort on my end.
- AWS's load balancer has:
  - Guarantees that it will be working
  - Takes care of upgrades, maintenance, HA

## Auto scaling group

- Use an AMI to scale in/scale out instances
- Uses health checks to remove unhealthy instances
