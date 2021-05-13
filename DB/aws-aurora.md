# AWS Aurora

The same as the other RDS engines, except:
Supports IAM database authentication, similar to Neptune. Attach identity policy to IAM principals that allow rds-db:connect for a resource that is a particular database user you create in particular way in the DB. You manage user permissions within the DB as per normal - IAM is just for authentication. You get a 'token' from the RDS API by specifying the db and user, then use the token in place of the user's password when connecting normally.
Uses normal VPC security groups to control access within a VPC. Has its own 'DB security group' to control access from outside the VPC - either security groups in other VPCs/accounts or the internet? The other RDS engines only use DB security groups in EC2 classic when a VPC isn't available.
