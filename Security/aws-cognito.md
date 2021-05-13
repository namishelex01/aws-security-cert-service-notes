* [**Cognito**](https://aws.amazon.com/cognito/faqs/)
    * User Pools
        + Free up to 50k monthly active users
        + OAuth user tokens
    * Identity Pools
        + Mapping between federated user IDs and Cognito user IDs. Per pool.
        + Grants temporary AWS creds (either directly from federation, or in exchange for a user pool token)
        + IAM Roles assigned based on: mappings defined for a user pool group / rules / guest
    + API Gateway has direct support for Cognito tokens (no need for identity pool)
    + Sync store - key/value store per identity
    + [Common scenarios](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-scenarios.html)
    + Various soft limits e.g. API calls/s, groups/pool, etc. No limit on number of users.

