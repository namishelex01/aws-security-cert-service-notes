# AWS SSM

Group resources of different types together based on a query, e.g. an application.
Many features require the Agent installed - many AWS AMIs include it by default. EC2 instances need an instance profile for a role that has the necessary permissions to allow the agent to interact with SSM.
Insights dashboard - per resource group
Shows CloudTrail, Config, software inventory, and patch compliance
Can integrate CloudWatch dashboards, Trusted Advisor notificaitons, Personal Health Dashboard
Potentially useful for understanding baseline usage patterns to contrast with during an incident
Inventory - applications, files, network configurations, Windows services, registries, more
Automation
documents of tasks to run; scheduled, triggered, or manually launched
Approval feature - configure approvals required (via the console) before it continues
Documents can have roles, and users can have permission to run documents - nice restriction of privileges to particular tasks
Run command
Sometimes called EC2 run command
Logs via CloudTrail
Can be triggered by CloudWatch Events
Session Manager - browser based shell w/ IAM & CloudTrail
Can log session data to S3 and/or CloudWatch Logs
Patch Manager
State Manager - specify OS configuration, rollout schedule, compliance reporting
Parameter store
Can be tagged + organized in a hierarchy.
KMS for encryption - users need KMS permissions to use the corresponding CMK (can restrict using a condition on kms:EncryptionContext to just particular parameters)
IAM resource per-parameter
10k params per account
Patch Manager and State Manager can operate on on-prem instances too
Lots of resources, no resource-based policies
The CloudWatch Agent can send SSM actions on the host to CloudWatch Logs
