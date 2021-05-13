* [Redshift](https://aws.amazon.com/redshift/)
    + Cluster management with IAM.
    + Database user accounts for DB permissions (SQL).
    + With custom Amazon Redshift JDBC or ODBC drivers, you can authenticate via IAM and get temporary DB user creds. Gives access to existing users or creates new users (groups specified via claims).
    + Lots of resources, main one is a cluster. No resource based policies. Managed policies to give access to all resources - `AmazonRedshiftFullAccess` and `AmazonRedshiftReadOnlyAccess`
    + Cluster are associated with 1+ security groups. Doesn't appear as an interface in a subnet. Contrast with RDS and DynamoDB - all different combos of network access control.
    + Audit logs, disabled by default, -> S3 (as well as the standard CloudTrail logs). Bucket policy has to allow putobject and getacl to a specific user from a redshift AWS account that varies by region: `arn:aws:iam::<redshift regional account id>:user/logs`. If creating the bucket via the console, it does that for you.
    + Optional encryption at rest. With KMS or CloudHSM Classic (only). Big symmetric encryption key heirarchy.
