# Route 53

Managed Domain Name System (DNS)

DNS is a collection of rules and records which helps clients understand how to reac a server through URLs

Some common records:

A: URL to IPv4
AAAA: URL to IPv6
CNAME: URL to URL
Alias: URL to AWS resource


1. User requests http://some-domain.com
2. Route 53 responds with IP: 32.45.87.21 (A record: URL to IP)

Application server lives at 32.45.87.21

3. User now makes requests to 32.45.87.21 with host http://some-domain.com
4. Application responds with HTTP response

Has advanced features such as:
- Load balancing (through DNS aka client load balancing)
- Health checks
- Routing policies

Costs $0.50 per month per hosted zone

## CNAME vs Alias

Example:
You have a load balancer or cloudfront resource which expose an AWS URL: alb1-292.us-east-1b.elb.amazonaws.com and you want it to point to myapp.somedomain.com

CNAME
- Points a URL to any other URL (api.somedomain.com => anotherapi.something.com)
- Works only for NON root domain (must be somethinghere.domain.com)

Alias
- Points a URL to an AWS resource (api.something.com => amazonaws.com)
- Works for root domain AND non root domain
- Free of charge + has native health check 

# 3rd Party Registrar with Route 53

If you buy your domain from somewhere other than Route 53:
1. Create a Hosted Zone in R53
2. Update NS records on 3rd party website to use Route 53 name servers


Domain registrar != DNS
But each domain registrar comes with some DNS features
