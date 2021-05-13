* [Certificate Manager](https://aws.amazon.com/certificate-manager/faqs/)
    + Issuance can take a few hours
    + Email or DNS validation (CloudFormation only supports email validation)
    + Validates DNS CA Authorization records first
    + Certs are region-locked, unless CloudFront is used (w/ Virginia)
    + Private keys are KMS protected - CloudTrail shows services using KMS to get the keys
    * Private CA
        + Allows export of the private key, whereas public standard only integrates with AWS services

