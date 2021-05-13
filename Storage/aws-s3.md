* [**S3**](https://aws.amazon.com/s3/)
    * Monitoring
        + CloudTrail by default records bucket-level actions
        + Can enble CloudTrail logging of object-level actions by setting that property on a bucket in S3 (can choose read/write)
        + Server access logging - separate audit log, configured per-bucket, that stores events in a bucket. Destination bucket needs a special ACL (see ACL section). Best-effort delivery.
    + Buckets and Objects are the main resources, each have various subresources (versioning, policies/acls, ...)
    + Buckets are truly global - no region or account ID in their ARN
    + The account that uploads objects owns them - even if the bucket is owned by a different account! Bucket owner pays for storage, manages storage class, and can delete or deny access to any object.
    + [Access control](https://docs.aws.amazon.com/AmazonS3/latest/dev/how-s3-evaluates-access-control.html) logic is complex. That page doesn't include "block public access" logic.
        + User needs to have permission - using identity policies (or user is the root of an account)
        + For bucket operations: bucket needs to have permission - either just bucket policy/acl for user in a different account, or both bucket policy/acl and identity policy if user is in the same account
        + For object operations: User has to have permission (or be root). Bucket policy/acl has to _not deny_. Object ACL (or bucket policy) has to allow. Three different account contexts in play - the user's account (IAM), the bucket's account (for bucket ACL/policy & identity policy if same-account), the object's account (for object ACL).
    * Bucket policies
        + Bucket resource-based policy.
    * ACLs
        + Bucket and object resource-based policy
        + Default ACL grants the owner account full control
        + List of grants, each grant gives a grantee (an AWS account or predefined group) a permission
        + Grantee groups: Authenticated Users group - _any_ AWS user. All Users group - incl anonymous. Log Delivery group - S3 audit logs.
        + Permissions: READ, WRITE (only applies to buckets - allows overwriting and deleting objects), READ/WRITE ACL, FULL CONTROL (all of the above)
        + Don't use bucket ACLs except for allowing write access to the Log Delivery Group for access logging. This is the only way.
    * Block Public Access
        + Applied to specific buckets, or all buckets in an account
        + BlockPublicAcls - can't create new public bucket or object ACLs
        + IgnorePublicAcls - existing (and new) public ACLs are ignored
        + BlockPublicPolicy - can't create public bucket polciies (only really works if applied account-wide, otherwise you can undo it via a bucket policy that allows modifying this policy...)
        + RestrictPublicBuckets - blocks all anonymous and cross-account access to a bucket
    + Query string authentication - instead of using the authorization header, you specify the access key ID and signature in 
    * Event notifications
        + Per bucket.
        + Sources: object creation, deletion, restoration from Glacier, and loss (for reduced redunadancy class)
        + Destinations: SNS topic, SQS queue, Lambda
    + Versioning
        + Enable on a bucket, then all object versions (including deleted one) remain available. Bucket owner can permanently delete.
        + Object lock: can't be deleted or overwritten until a particular date. Governance mode - needs s3:BypassGovernanceMode to override; Compliance mode - can't be overridden, even by root. Legal Hold - no end date (separate perm needed to override). Applies to an individual object version.
        + MFA delete: have to provide a TOTP code to delete (separate to IAM MFA) in `x-amz-mfa` header
    * Lifecycle policies 
        + Transition action - change storage class
        + Expiration action - delete
        + e.g. archive old versions to glacier, then delete.
    * Encryption
        + SSE-S3  - pure S3 managed encryption
        + SSE-KMS - standard KMS integration like other services
        + SSE-C   - you send the plaintext encryption key in the request (!)
        + The SDKs also ease support for client-side encryption
