* [Secrets manager](https://aws.amazon.com/secrets-manager/faqs/)
    + Also see: Systems Manager Parameter Store - no rotation features, but free.
    + Automatic rotation for AWS RDS, DocumentDB, Redshift
    + Lambda functions to rotate other types
    + 4kb limit on secrets (JSON docs)
    + Encryption at rest via KMS. (for cross-account access to a secret, must use a custom CMK that the principal in the other account can use)
    * [Policies](https://docs.aws.amazon.com/secretsmanager/latest/userguide/auth-and-access.html)
        + Resource-based (action+principal) and identity-based (action+resource) policies.
        + `arn:aws:secretsmanager:<region>:<account-id>:secret:optional-path/secret-name-6-random-characters`
        + ```json
            {
                "Sid" : "Get current TestEnv secrets",  
                "Effect": "Allow",
                "Action": [ "secretsmanager:GetSecretValue" ],
                "Resource": "arn:aws:secretsmanager:<region>:<account_id>:secret:TestEnv/*",
                "Condition" : { 
                    "ForAnyValue:StringLike" : {
                        "secretsmanager:VersionStage" : "AWSCURRENT" 
                    } 
                }
            }```
        + Condition keys include `secretsmanager:ResourceTag/<tagname>`, `secretsmanager:VersionStage`
        + Configuring rotation requires creating and assigning a role to a Lambda function, which needs e.g. IAMFullAccess
