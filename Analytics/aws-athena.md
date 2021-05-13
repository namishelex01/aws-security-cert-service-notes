* [Athena](https://aws.amazon.com/athena/faqs/)
    + SQL queries over data in S3 after you define a schema. Including (optionally compressed) JSON & CSV
    + Integrates with Glue's Data Catalog - a more featureful version of Athena's built in Data Catalog which supports fine-grained permissions.
    + Charged per query (volume of data scanned)
    + Security model uses both athena:* permissions for queries and data models, and then the underlying S3 permissions
    + Can query encrypted data that uses S3 or KMS managed keys. Can encrypt results.
    + Athena is better than Redshift for querying smaller datasets without pre-processing.
    + CloudTrail can automatically create Athena tables for you, and AWS are keen to push Athena as an ideal CloudTrail analysis tool. Other good candidates: VPC flow logs (if sent to S3), CloudFront, ELB.

