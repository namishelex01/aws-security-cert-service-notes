* [EFS](https://aws.amazon.com/efs/)
    + NFS filesystem
    + Standard posix permissions
    + Mount targets appear as endpoints in a VPC, so Security Groups can control access
    + IAM only used for administration
    + transparent encryption at rest with KMS (could monitor compliance with a CloudWatch alarm over CloudTrail logs)
    + NFS over TLS is an option with the EFS mount helper (stunnel)
