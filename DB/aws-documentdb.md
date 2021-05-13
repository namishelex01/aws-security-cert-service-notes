* [DocumentDB](https://aws.amazon.com/documentdb/)
    + Similar to RDS: TLS from the RDS root; KMS encryption at rest; master user + mongodb user mgmt; IAM identity policies for management; VPC security groups; endpoints on multiple subnets/AZs; cloudtrail
    + arns follow the RDS format
    + Auditing can be enabled to send events to CloudWatch Logs. Categories: connection, data definition language (DDL), user management, and authorization
