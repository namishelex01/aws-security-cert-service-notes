# AWS Config

Resource inventory, configuration history, and configuration change notifications
Configuration changes or deviations -> SNS, CloudWatch Events, console dashboard, S3
Regional, but can aggregate data across (a limited set of supported) regions and accounts. Can't centrally manage rules.
Inspects software running on SSM managed EC2 instances, incl OS version, installed apps, network config.
Configuration changes sent to 'delivery channel' - S3 bucket & SNS topic
Console provides a timeline view of configuration changes
AWSConfigRole is the managed audit role; also needs permisisons for the SNS topic & S3 bucket.
Rules
Continuously evaluate configs against rules
Retrospective and non-enforcing
Custom rules in Lambda
Soft limit of 50 active rules
Periodic (hourly to daily) or change-triggered. Change-triggered must be constrained by tag/resource type/resource id
