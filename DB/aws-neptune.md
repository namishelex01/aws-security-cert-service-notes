* [Neptune](https://aws.amazon.com/neptune)
    + HTTPS access
    + Encryption at rest with KMS
    + Interface appears in at least two subnets spanning two AZs in a VPC, interfaces have security groups.
    + CloudTrail events appear as though they are from the RDS service not Neptune - it shares some underlying management infrastructure.
    + Optional audit logs, view or download from the console (no other service integrations, strangely)
    + IAM for management. Permissions are a subset of rds permissions all the actions are `rds` actions. Can constrain to just neptune with a condition of `rds:DatabaseEngine = graphdb`
    + Has a very unique hybrid model where you can authenticate with IAM, and define identity policies that allow access. Limited - no condition keys, no fine grained access (only a single `neptune-db:*` action). Pretty confusing when compared to the previous point. HTTP requests then need to be signed with standard AWS v4 signatures that you construct yourself.
