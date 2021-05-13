* [Backup](https://aws.amazon.com/backup/)
    + Centralise backups across RDS, DynamoDB, EBS, EFS, Storage Gateway. Uses those services' native capabilities (snapshots etc)
    + Can be encrypted in transit and at rest. Uses the service's native encryption capabilities, or for EFS where the backup functionality comes from Backup itself, it does the usual KMS encryption. Other than EFS, encryption depends on whether the source is encrypted (note DynamoDB tables are always encrypted at rest).
    + Resources: plans, vaults, recovery points. 
    + Resource-based policy for vaults, but these only constrain _vault_ access, not access to the underlying backup like an EBS or RDS snapshot.
