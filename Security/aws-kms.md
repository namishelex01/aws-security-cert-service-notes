## [**KMS**](https://aws.amazon.com/kms/faqs/)
 
### Key policies

+ Required. Also different evaluation logic to standard IAM 
 + Eg. - if the key policy doesn't allow, then the request is denied regardless of identity policies.
+ Resource: "*" - this CMK
+ Principal: accounts/users/roles/services. 
 + Not groups! Have to use IAM identity policies to manage access via groups (or group -> assumerole).
+ Default policy for API-created CMKs allows `kms:*` for the account / root user. This ensure it doesn't become unmanageable, and also _enables_ identity based IAM policies - without it IAM policies are ineffective.
+ Default policy for console created keys also allows you to specify:
   + Roles/Users who are Key Administrators, who can manage it - incl change its policy
   + Roles/Users/other AWS accounts who are Key Users. They can encrypt/decrypt/generatedatakey, and manage grants for AWS services using the `kms:GrantIsForAWSResource` condition
 
### IAM/identity policies
   + Required for non-key specific tasks list ListKeys, ListAliases, and CreateKey
   + Required to use the console
+ Bunch of [KMS-specific condition keys](https://docs.aws.amazon.com/kms/latest/developerguide/policy-conditions.html?shortFooter=true#conditions-kms) that can be used in either policy type.
   + `kms:ViaService` to prevent direct API use or block specific service use. All AWS managed CMKs use it to restrict access to the creating service.

### Grants
+ Another resource-based policy attached to keys(CMKs).
+ Allow-only, no Deny.
+ "grantee principal" - who can use the CMK. 
+ "retiring principal" - who can revoke the grant
+ Actions: drawn from using the key, and creating further grants
+ Grant tokens: passed back when creating a grant, allows grantees to use the grant even before it has fully propagated. Not secret, no security impact, just practical.

* Key usage -> CloudTrail
* AWS services use wrapped data keys with KMS - 'envelope encryption'
* APIs expose raw encrypt/decrypt operations, <4kb

### CMKs
   + AES-256
   + CMKs are stored in HSMs (140-2 level 2)
   + AWS managed CMKs you have no control over. Customer managed ones you can set policies.
   + Imported CMKs can be deleted immediately and can have an expiry time.
   + 1000 CMKs per region
   + Keys are region-specific. For a [multi-region solution](https://aws.amazon.com/blogs/security/how-to-use-the-new-aws-encryption-sdk-to-simplify-data-encryption-and-improve-application-availability/), encrypt a single data key under CMKs in different regions.
   + Customer controlled CMKs can be enabled/disabled
   + Automatic annual key rotation can be enabled for customer controlled keys that don't use imported key material.

### Custom key store
   + Uses CloudHSM
   + Can't import or automatically rotate keys - otherwise the same management as normal key stores
   + Only for customer managed CMKs
   + You're responsible for availability
   + Manual rotation: create key and remap key alias

### CloudHSM
   + Single tenant 140-2 level 3 HSM - compliance
   + CloudHSMs appear in a VPC
   + Audit options beyond CloudTrail - CloudHSMs log locally and copy to CloudWatch
   + PKCS11 etc interfaces (as well as using as a custom key store)

+ Each region has a FIPS 140-2 validated endpoint (uses openssl fips module) and a standard endpoint
+ AES-128 or AES-256 data keys
+ Crypto operations accept an optional _encryption context_, which is used as additional authenticated data (AAD) in the operation. 
   + If differs then decryption fails. Included in CloudTrail logs. Example used by S3:
   ```json
   "encryptionContext": {
       "aws:s3:arn": "arn:aws:s3:::bucket_name/file_name"
   },
   ```

