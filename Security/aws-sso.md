* [SSO](https://aws.amazon.com/single-sign-on/faqs/)
    + Free
    + Primary use case: manage multi-account access with Organizations.
    + Additional use case: SSO to other applications via SAML 2 (custom or a bunch of built-in integrations)
    + IAM identity provider created in member accounts for SSO. Also service-linked roles created to allow SSO to manage Roles
    + Sign-ins logged to CloudTrail
    * Directories
        + Native directory - default. Create users & groups within SSO
        + AWS Directory Service - Managed AD & AD Connector (not simple AD)
        + Only a single directory can be connected
    * Permissions sets
        + collections of policies.
        + Implemented as Roles in member accounts.
        + Limit of 20 per account.
        + Ref 10 AWS managed policies, or use an inline policy
    + Control access by mapping users/groups (from the attached directory) to permissions sets & accounts. This data is held in SSO, not the directory.
    + No API!
    + For CLI access, SSO user portal gives you temporary creds for the Roles you have access to
