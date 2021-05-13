* [CloudHSM](https://aws.amazon.com/cloudhsm/faqs/)
    + Advertised as only suitable when you have contractual/regulatory constraints.
    + Only option for SQL Server and Oracle transparent database encryption (but not AWS RDS Oracle! only instances running on EC2. RDS Oracle  only works with CloudHSM Classic). Also works with Redshift.
    + PKCS#11, JCE, CNG
    + FIPS 140-2 Level 3 certified
    + KMS can use it as a key store - see KMS section
    + Each instance appears as network resource in VPC; client does load-balancing.
    + [[HSM] Server] <-TLS-in-TLS-> [client] <-p11 etc-> [app]
    + HSM users authenticate with username + password
    + CloudTrail for provisioning API calls; CloudWatch Logs for HSM logs

