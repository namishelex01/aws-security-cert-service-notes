# AWS DynamoDB

Optional encryption at rest integrated with KMS
Main resource is a table. No resource based policies. Full access to a table requires access to not just the table/<name> resource, but also table/<name>/*
Some predefined policies: AmazonDynamoDBReadOnlyAccess, AmazonDynamoDBFullAccess - custom policies with resource constraints are better
Several condition keys for fine-grained access including: dynamodb:LeadingKeys, dynamodb:Select, dynamodb:Attributes
Example fine-grained permission: you can only access items where the partition key matches your own (web identity) user ID, by using LeadingKeys and a substitution variable.
Get and Put API calls are not logged to CloudTrail - management things are like describe, list, update, create
Has a VPC endpoint you can use
Integration with Cognito: identity pool with roles configured; roles have appropriate policy to (a) allow cognito to assume them and (b) perform desired DynamoDB actions.
