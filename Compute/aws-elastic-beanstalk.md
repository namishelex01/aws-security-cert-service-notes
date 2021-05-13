* [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)
    + Management wrapper around EC2, S3, EBS, RDS
    + Publicly available by default - configure to use a VPC to limit access
    + Beanstalk service role to manage other services. Instance profile - role used by instances to get the app, write logs, etc
    + Logs stored locally, can be configured to use CloudWatch Logs
