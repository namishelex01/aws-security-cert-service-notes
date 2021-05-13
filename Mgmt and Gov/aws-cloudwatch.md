# AWS Cloudwatch

Logs
CloudWatch Agent can be installed on a host (e.g. via SSM) to push logs to CloudWatch Logs. Troubleshooting info.
Log group: a collection of log streams that share the same retention, monitoring, and access control settings
Log stream: a sequence of log events that share the same source
Logs last forever unless you set a retention period on a group
Subscription filters: define a filter pattern that matches events in a particular log group, send them to Kinesis Data Firehose stream, Kinesis stream, or a Lambda function.
Can export log groups (in a particular time range) to S3. Not real time.
Can receive events from other account by creating a 'destination' in CloudWatch, which references a receiving Kinesis stream? The destination has a resource-based policy that controls which accounts can write to the destination. CloudWatch Logs on the sender side can then stream to the other account.
Logs Insights
Limited query language for analysis and visualization of data in CloudWatch Logs
Much more powerful than the native CloudWatch Logs interface
Events
Rules that trigger from either event patterns or a schedule
Rules send JSON to one or more targets
Has other capabilities (metrics, alarms, scaling)
