# AWS SQS

Polling, vs SNS's push mechanism
Standard queues might reorder messages or deliver them multiple times
Has its own resource-based security policy, that predates IAM? Looks similar to IAM policies. Only resource is a queue.
Can subscribe to SNS topics
Can trigger Lambda functions on message receipt
Uses KMS for optional encryption