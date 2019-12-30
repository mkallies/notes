# Monitoring

## CloudWatch

Metrics

- CloudWatch provides metrics for every service in Aws
- Metrics belong to namespaces
- Dimension is an attribute of a metric
- Up to 10 dimensions per metric
- Can create CloudWatch dashboards of metrics

EC2 Detailed monitoring

- EC2 metrics are updated every 5 minutes
- With detailed monitoring ($) you get every 1 minute
- AWS free tier offers 10 detailed monitoring metrics
- EC2 memory usage is by default not pushed and must be done yourself ( you can use Custom Metrics )

CloudWatch Custom Metrics

- Can define and send your own custom metrics to CloudWatch
- Ability to use dimensions (attributes) to segment metrics
  - instance id
  - environment name
- Metric resolution
 - standard: 1 minute
 - High resolution: up to 1 second (StorageResolution API parameter, higher cost)
 - Use API call PutMetricData
 - Use exponential back off in case of throttle errors

CloudWatch Dashboards

- Great way to display key metrics
- Dashboards are global
- Dashboards can include graphs from different regions
- Can change timezone and time range of dashboards
- Can setup automatic refresh (10s, 1m, 2m, 5m, 15m)

Pricing
  - 3 dashboards (up to 50 metrics) for free
  - $3/dashboard/month after free tier

Logging
 - Can send logs to CloudWatch via the AWS SDK
 - Can collect from:
  - Elastic Beanstalk - collection of logs from application
  - ECS - collection from containers
  - AWS Lambda - collection from function logs
  - VPC flow logs - VPC specific logs
  - API gateway
  - CloudTrail based on filter
  - CloudWatch log agents - on EC2 machines
  - Route53 - log dns queries

Can send logs to
 - Batch exporter to S3 for archival
 - Stream to ElasticSearch cluster for more analytics

Log storage architecture
  - Log groups: arbitrary name, usually representing an application
  - Log stream: instances within application / log files / containers

Can define log expiration policies (never expire, 10 days, etc)

Using AWS CLI we can tail CloudWatch logs

To send logs to CloudWatch, make sure IAM permissions are correct

Security: encryption of logs using KMS at the group level

Using Metric Filter & Insights
