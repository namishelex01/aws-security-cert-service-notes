* [**Cognito**](https://aws.amazon.com/cognito/faqs/)

Amazon Cognito provides authentication, authorization, and user management for your web and mobile apps. Your users can sign in directly with a user name and password, or through a third party such as Facebook, Amazon, Google or Apple.

 * User Pools
     + User directories that provide sign-up and sign-in options for your app users
     + Free up to 50k monthly active users
     + OAuth user tokens
 * Identity Pools
     + Mapping between federated user IDs and Cognito user IDs. Per pool.
     + Grants temporary AWS creds (either directly from federation, or in exchange for a user pool token)
     + IAM Roles assigned based on: mappings defined for a user pool group / rules / guest
 + API Gateway has direct support for Cognito tokens (no need for identity pool)
 + Sync store - key/value store per identity
 + [Common scenarios](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-scenarios.html)
   + Authenticate with a User Pool
   + Access Server-side Resources with a User Pool
   + Access Resources with API Gateway and Lambda with a User Pool
   + Access AWS Services with a User Pool and an Identity Pool 
   + Authenticate with a Third Party and Access AWS Services with an Identity Pool
   + Access AWS AppSync Resources with Amazon Cognito
 + Various soft limits e.g. API calls/s, groups/pool, etc. No limit on number of users.

