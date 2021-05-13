* [**CloudTrail**](https://aws.amazon.com/cloudtrail/)
    + Also logs Cognito events, step function logs, and CodeDeploy
    + Logs to S3 and/or CloudWatch Logs
    + Without creating a trail, the event history shows 90 days but excludes various events including all read events
    + A [small number](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-unsupported-aws-services.html) of services don't log to CloudTrail, notably SimpleDB
    + Trails by default don't include data events (incl S3 object activity and Lambda execution). Can specify those resources you want to record.
    + Trails are regional, but you can create a global trail which creates identitical trails in all regions. Limit of 5 trails per region.
    + eventSource: what service produced the event.
    + Can enable SNS notifications for when a new log _file_ is produced
    + Can set up CloudWatch metric filters for certain events to trigger a CloudWatch Alarm
