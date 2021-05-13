* [**Organizations**](https://aws.amazon.com/organizations/faqs/)
    + Organizational Units (OUs) divide up the 'administrative root'
    + Accounts can only be in one OU, and OUs can only be in one OU. But they can be nested up to 5 levels.
    * Service Control Policies (SCPs)
        + Which IAM policy Actions can be used in the account.
        + Applied to the root, to an OU, or to an account
        + Implicit and explicit Deny.
        + All statements: Version, Statement, Sid, Action, and Effect:Allow/Deny
        + Allow statements: no conditions, Resources must be '*'
        + Deny statements: support conditions and resources and NotAction
        + No principal - implicitly the accounts it's applied to
        + Is a whitelist, but can simulate a blacklist with Allow Action:'*' and another Deny statement
        + FullAWSAccess (allow *) is automatically attached to the root and new OUs. You can remove it.
        + Use policy simulator in member accounts to test effect
    * Trusted access
        + service-linked roles get created in member accounts as needed. Authorized via master account.
        + CloudTrail can create an [organizational trail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/creating-trail-organization.html), for all events in all member accounts. Member accounts can't modify it.
    + Landing Zone account structures, incl logging & security accounts

