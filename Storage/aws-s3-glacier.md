* [S3 Glacier](https://aws.amazon.com/glacier/)
    + Encrypted by default
    + Value access policies - resource based policy attached to a vault. Like a bucket policy.
    + Vault lock policies - a vault access policy that can be locked to prevent changes to it
    + Other than the global ones and tags, supports `glacier:ArchiveAgeInDays` condition key - nice in combo with the `glacier:DeleteArchive` action
    + Retrieval requires job initiation then getting the output from the job
    + Data retrieval policy: a resource-based policy for regions? They don't describe it as such, but each region can have one policy that constrains Glacier retrievals to free tier / maximum transfer rate / unlimited.
