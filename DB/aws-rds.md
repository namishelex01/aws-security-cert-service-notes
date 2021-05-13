* [RDS](https://aws.amazon.com/rds/)
    + IAM controls database instances. Each instance type has its own permission model for managing the database - a master user is created with the instance.
    + Lots of different resources. The main one is an instance - `db` in the arn. No resource based policies.
    + 'RDS Encryption' - encryption at rest, set during creation, uses KMS. Covers database, backups, replicas, snapshots.
    + Transparent data encryption for SQL Server and Oracle with CloudHSM
    + There's a single root for all RDS database TLS certs; each engine uses its own method for connecting over TLS
    + Manifests as network interfaces in subnets with security groups attached to the interfaces. You specifc a "db subnet group" - a collection of subnets which it can use to put interfaces in.
    + "Publicly accessible" option controls whether there is a publicly resolvable DNS name for the instance. Still needs appropriate security group rules.
