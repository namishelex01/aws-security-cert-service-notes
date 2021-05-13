* [**EC2**](https://aws.amazon.com/ec2/)
    * AMIs
        + LaunchPermission attribute - which _accounts_ can use the AMI.
    * [Keypairs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)
        + Create or import - 2k RSA.
        + Independent of instances, but each instance is associated with 1+ keys
        + Linux: it's just an SSH key
        + Windows: upload the private key to the ec2 console to decrypt the default admin password so you can RDP in...
        + Subsequent management: tinker with the `authorized_keys` file
    + [Resources and condition keys](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-policy-structure.html)
    + Instance store - hard disk attached to the instance; reset when the instance is stopped. Not encrypted - could use host software disk encryption for a temporary data partition.
    + Instance profile - credentials for a role available to the instance (see IAM section)

