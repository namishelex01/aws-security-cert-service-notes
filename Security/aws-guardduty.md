* [**Guard Duty**](https://aws.amazon.com/guardduty/faqs/)
    + Uses CloudTrail, VPC Flow Logs, and DNS Logs (if EC2 instances are configured to use Route 53 resolvers - the default). Doesn't require you to enable them!
    + ^^ meta-data, + AWS' threat intelligence - domains & ips, + ML
    + Pricing per volume of data analyzed
    + Looks for reconnaissance, (ec2?) instance compromise, account compromise
    + Findings -> GuardDuty console (for 90 days) + CloudWatch Events. Findings in JSON format similar to Macie & Inspector
    + Regional. Can aggregate via CloudWatch Events to push to a central store
    + CloudWatch events -> SNS topic (-> email) / Lambda (->S3)

