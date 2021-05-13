# AWS Trusted Advisor

7 free checks, all checks with appropriate support plan.
API; Console; Weekly notification email with summary of findings
Can exclude resources from all checks. Can't suppress individual checks.
Cost optimization, security, service limits, fault tolerance, performance
Security checks:
Security group open access to specific high-risk ports
Security group unrestricted access
Open write and List access to S3 buckets
MFA on root account
Overly permissive RDS security group
Use of cloudtrail
Route 53 MX records have SPF records
ELB with poor or missing HTTPS config
ELB security groups missing or overly permissive
CloudFront cert checks - expired, weak, misconfigured
IAM access keys not rotated in last 90 days
Exposed access keys on GitHub etc
Public EBS or RDS snapshots
Missing or weak IAM password policy