* [Secrets manager](https://aws.amazon.com/secrets-manager/faqs/)
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

* [Systems Manager Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html)
    + No rotation, but free
    + store data = passwords, db strings, AMI IDs, license codes
    + Features
        + Change notification
        + Organize and control access
        + Label versions
        + Data validation
    + String, StringList, and SecureString parameters
    + SecureString data encryption = AWS KMS key
    + Parameter Store supports only symmetric KMS keys
    + Accessible from -> EC2, ECS, Secrets Manager, Lambda, CloudFormation, CodeBuild, CodePipeline, CodeDeploy

* Difference between Systems Manager Parameter Store vs Secrets Manager

| | SSM Param Store | Secrets Manager |
|--|--|--|
| Store values upto 4096 chars| :white_check_mark: | :white_check_mark: |
| Values can be encrypted using KMS | :white_check_mark: | :white_check_mark: |
| Can be referenced in Cloudformation | :white_check_mark: | :white_check_mark: |
| Built-in password generator |  | :white_check_mark: |
| Automated secret rotation | | :white_check_mark: |
| No additional cost | :white_check_mark: | |
| Cross-account access | | :white_check_mark: |
