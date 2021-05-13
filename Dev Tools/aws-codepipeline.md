# AWS Codepipeline

Resource-level permissions for pipelines, and their stages and actions.
Can integrate with GitHub via OAuth
CloudWatch Events for pipeline state changes - started, failed, etc.
Supports interface VPC endpoint
Trigger from, e.g.: CloudWatch Events (many options, e.g. S3 bucket upload, schedule), webhooks (e.g. github), manual
Deploy to, e.g.: CloudFormation, S3, ECS, Service Catalog
