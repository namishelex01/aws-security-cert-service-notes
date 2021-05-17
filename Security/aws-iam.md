* [**IAM**](https://aws.amazon.com/iam/faqs/)
    * Users, Groups, Roles
        + Roles for EC2 instances
            + creds found in `http://169.254.169.254/latest/meta-data/iam/security-credentials/<role/instance profile name>`
            + To launch an instance, users need iam:PassRole for the relevant roles.
            + Can be attached at launch or later.
            + Auto rotation, built in support for obtaining the creds when using CLI & SDKs
        + Service linked role - predefined policy granting service what it needs; immutable trust policy.
        + Role trust policy: what principals (account/user/role/service/federated user) can sts:AssumeRole. IAM users/roles also need an identity policy that allow them to assume the role.
        + Assumed role ARN: `arn:aws:sts::AWS-account-ID:assumed-role/role-name/role-session-name`, where the session name might be the EC2 instance ID, or the IAM username, for example.
    * Access keys
        + Rotate by creating second access key, start using it, check last used date of old one, make old one inactive, then delete it
        + Trusted advisor can look for overly long-lived access keys
    * Policies
        + Resource based policies
            + Specifies a Principal.
            + Can't be managed policies - always inline.
            + Not actually IAM policies at all - just usually use the same policy language
            + Notable ones: Organizations (SCP); S3; API Gateway; Lambda; KMS 
        + Identity based policies (aka IAM policies)
            + Attached to a user/group/role - implicit Principal
            + Limit of 10 managed policies can be attached
            + Versions - up to 5, you set which is the 'default' for customer managed policies. Inline policies don't have versions.
        * [Permissions boundaries](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html)
            + Set the maximum permissions that an identity-based policy can grant to an IAM entity
            + Unlike SCPs, can specify resources and use conditions
        + Service Control Policies (SCPs) - see Organizations
        + Session policies - like a permission boundary, optionally passed programatically as part of AssumeRole*
        * [Evaluation logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html) - but there are special cases not listed here, e.g. KMS, S3
        * Conditions
            * Operators
                + Date, Numeric, String, Bool, Binary (b64), IpAddress, Arn, Null (key:true - key doesn't exist, key:false - key does exist and isn't null)
                + operators are ANDed, multiple values in an operator are ORed
                + ...IfExists returns true if key doesn't exist
                + Set operators for keys with multiple values - ForAllValues:<operator>... ForAnyValue:<operator>...
            + All services: time, MFA, secure transport, user agent
            + aws:source{Vpc,Vpce (endpoint),Account,Arn,Ip}
            + aws:PrincipalOrgID - instead of listing lots of accounts, just use the Org. In resource policies - Principal:*, then this condition
            + aws:PrincipalTag/<tag-key> - you can tag users and roles. Also service:ResourceTag and aws:RequestTag (control what tags users can use when tagging resources).
            + aws:PrincipalType
            + aws:RequestedRegion
            + aws:userid aws:username
        * Policy variables
            + Use in resource element and string operators in conditions
            + Basically the same set of variables as global conditions. aws:username etc.
        * (Not)Principal
            + AWS - users, roles, accounts
            + Federated - just "this principal authenticated with this provider" - no info on the role
            + Service - in trust policies
            + AWS:* - IAM identities (not services)
            + NotPrincipal rarely, and not with Allow as v fragile. NotPrincipal+Deny acts like a whitelist due to policy eval rules.
        + NotAction - matches everything except the list of actions. With Allow is very broad - combine with a resource constraint to make it more selective.
        * Resource
            + Wildcards - *? - don't span segments
            + NotResource + Deny: blacklist. NotResource + Allow: risky - allows all others incl. future ones.
    * Access advisor
        + When did an entity last use a permission
        + For each of User, Group, Role, and Policy
    * Federation
        + SAML
            + Users gets SAML assertion from their IdP portal, uses STS to exchange it for temporary creds.
            + IdP maps users/groups to roles.
            + Requires config info including keys registered with both the IdP and AWS IAM
            + Use AWS SSO to access the console.
        + Web identity federation - just use Cognito. IAM does support it natively too though.
        + Active Directory - use Directory Service, setup roles that trust DS, assign users or groups to roles
    + [Service support](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html)
        + Of interest are services that have resource-based policies, services that don't have resource-level permissions, and services that don't support temporary creds
        + Notable resource-based policies: ECR; Lambda; S3 & Glacier; KMS; Secrets Manager; API Gateway; VPC endpoints; SNS; SQS; SES
        + Notable ones missing resource level permissions: CloudFront (no resource policies either)
        + ~everything that matters supports temporary credentials
    * Temporary credentials
        + Can't be revoked, but you can revoke an IAM user if they created the temporary creds, which invalidates them.
        + Include a token as well as access key & secret key. Token is appended to requests (header/query param)
        + Not regional
        + You can use AssumeRoleWithWebidentity as a less-featured alternative to Cognito w/ your users
    * Multifactor
        + No support for SMS any more.
        + U2F, virtual TOTP, hardware TOTP provided by AWS.
        + Root user can recover from lost second factor by verifying email address + phone number ownership.
        + APIs can require it by adding condition statements to identity or resource policies using `aws:MultiFactorAuthPresent` or `aws:MultiFactorAuthAge` (time since factor seen). Users then call STS to get temporary credentials that allow them to use the API. Doesn't work with root or U2f.
        + Doesn't work with federation

