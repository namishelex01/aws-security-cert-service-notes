# AWS Service Security Notes
An all-in-one-place collection of security information about all of the core AWS services.

These are the notes I created whilst studying for the [AWS Certified Security - Specialty](https://aws.amazon.com/certification/certified-security-specialty/) exam. They are intended as a knowledge check, reminder, and subject list for each AWS service. They are not intended as a primary learning source, and they assume an existing knowledge of security. I think if you can look through this list and feel confident that you are familiar with all of it, don't come away with a lot of follow up questions, and think you can recall most of it unaided, then you will probably pass the security certification exam. It worked for me, anyway!

I don't plan to actively maintain this document as AWS evolves - reader beware, the rate of change at AWS is high! I would like to correct any errors though - please do raise an issue. I'll also happily accept pull requests if you find yourself using it and wish to bring it up to date, or fix errors, or otherwise enhance it in any way.

Final caveat: this doesn't teach you how to be good at AWS security. See my blog post on [what I think the Security Speciality certification means](https://mykter.com/2019/05/04/aws-security-certification), and hence what this document aims to cover.

If you found this useful please [let me know](https://twitter.com/michael_macnair)!

<br><br>
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">AWS Service Security Notes</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/mykter/aws-security-cert-service-notes" rel="dct:source">https://github.com/mykter/aws-security-cert-service-notes</a>.

# Services
A complete list of the AWS security services, and selected additional AWS services of relevance to security (in particular, the security specialist certification). Taken from the [AWS product list](https://aws.amazon.com/products/) as of March 2019; if a category isn't listed it's because I thought none of the services in that category are particularly applicable.

Particularly important services from an exam perspective are in **bold**.

Security service links are to their FAQ pages, as a useful source of information on particular use cases and constraints that might be examined. Other service links are to their main product pages, but the FAQ pages often have good information including a security section too.

## Security

* [Artifact](https://aws.amazon.com/artifact/faq/)

* [Certificate Manager](https://aws.amazon.com/certificate-manager/faqs/)

* [Cloud Directory](https://aws.amazon.com/cloud-directory/faqs/)
 
* [CloudHSM](https://aws.amazon.com/cloudhsm/faqs/)

* [**Cognito**](https://aws.amazon.com/cognito/faqs/)

* [**Directory Service**](https://aws.amazon.com/directoryservice/faqs/)

* [Firewall Manager](https://aws.amazon.com/firewall-manager/faqs/)

* [**Guard Duty**](https://aws.amazon.com/guardduty/faqs/)

* [**IAM**](https://aws.amazon.com/iam/faqs/)

* [Inspector](https://aws.amazon.com/inspector/faqs/)

* [**KMS**](https://aws.amazon.com/kms/faqs/)

* [Macie](https://aws.amazon.com/macie/faq/)

* [**Organizations**](https://aws.amazon.com/organizations/faqs/)

* [Secrets manager](https://aws.amazon.com/secrets-manager/faqs/)
 
* [Security hub](https://aws.amazon.com/security-hub/faqs/)

* [Shield](https://aws.amazon.com/shield/faqs/)

* [SSO](https://aws.amazon.com/single-sign-on/faqs/)

* [WAF](https://aws.amazon.com/waf/faqs/)

## Analytics
(mostly of interest for their application to logs)

* [Athena](https://aws.amazon.com/athena/faqs/)

* [Elasticsearch service](https://aws.amazon.com/elasticsearch-service/faqs/)

* [Glue](https://aws.amazon.com/glue/faqs/)

* [Kinesis](https://aws.amazon.com/kinesis/)

* Redshift (see Database section)

## Application Integration

* [SNS](https://aws.amazon.com/sns/)

* [SQS](https://aws.amazon.com/sqs/)

## Compute

* [**EC2**](https://aws.amazon.com/ec2/)

* [Elastic Container Registry (ECR)](https://aws.amazon.com/ecr/)

* [Elastic Container Service (ECS)](https://aws.amazon.com/ecs/)

* [Lightsail](https://aws.amazon.com/lightsail/)

* [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)

* Fargate - see ECS

* [**Lambda**](https://aws.amazon.com/lambda/)

* [Elastic Load Balancing (ELB)](https://aws.amazon.com/elasticloadbalancing/)

## Customer Engagement

* [Simple Email Service (SES)](https://aws.amazon.com/ses/)

## Database

A comparison and summary of some of the security aspects of the various database offerings:

| **Database** | **Transport encryption**                                                               | **Encryption at rest**                           | **Audit**                                            | **DB Authentication**                                                                                         | **DB Authorization**                                                         |
|--------------|----------------------------------------------------------------------------------------|--------------------------------------------------|------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| RDS          | Rooted at global RDS certs, configuration is per-engine <br>[docs][rds-tls]            | KMS; TDE w/ SQL Server and Oracle - RDS managed key (used to be CloudHSM Classic)| per-engine log files | per engine user accounts - SQL                                                                              | per engine - SQL                                                             |
| DynamoDB     | Standard AWS HTTPS endpoint                                                            | KMS                                              | CloudTrail, excl. Get/Put <br>[docs][dynamodb-audit] | IAM only. Cognito possible. <br>[docs][dynamodb-cognito]                                                      | IAM identity policies - resources & condition keys <br>[docs][dynamodb-auth] |
| Redshift     | ACM managed certificate, redshift specific root <br>[docs][redshift-tls]               | KMS; CloudHSM Classic                            | S3 <br>[docs][redshift-audit]                        | DB user accounts - SQL; IAM with custom drivers <br>[docs][redshift-auth]                                     | SQL                                                                          |
| Neptune      | Publicly trusted Amazon root; mandated for some regions <br>[docs][neptune-tls]        | KMS                                              | Console <br>[docs][neptune-audit]                    | User accounts; or a limited IAM identity policy mechanism + request signing <br>[docs][neptune-auth]          | Engine-specific; or broad access if using IAM                                |
| Aurora       | Rooted at global RDS certs, configuration as per mysql/postgres <br>[docs][aurora-tls] | KMS                                              | mysql -> CloudWatch Logs <br>[docs][aurora-audit]    | User accounts; or an IAM authenticated API to obtain short lived passwords to connect <br>[docs][aurora-auth] | mysql/postgres - SQL                                                         |
| DocumentDB   | Rooted at global RDS certs, configuration as per MongoDB <br>[docs][documentdb-tls]    | KMS                                              | CloudWatch Logs <br>[docs][documentdb-audit]         | MongoDB user accounts                                                                                         | MongoDB standard                                                             |

[rds-tls]: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL.html
[dynamodb-audit]: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/logging-using-cloudtrail.html
[dynamodb-auth]: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/using-identity-based-policies.html
[dynamodb-cognito]: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WIF.html
[redshift-tls]: https://docs.aws.amazon.com/redshift/latest/mgmt/connecting-ssl-support.html
[redshift-audit]: https://docs.aws.amazon.com/redshift/latest/mgmt/db-auditing.html
[redshift-auth]: https://docs.aws.amazon.com/redshift/latest/mgmt/generating-user-credentials.html
[neptune-tls]: https://docs.aws.amazon.com/neptune/latest/userguide/security-ssl.html
[neptune-audit]: https://docs.aws.amazon.com/neptune/latest/userguide/auditing.html
[neptune-auth]: https://docs.aws.amazon.com/neptune/latest/userguide/iam-auth.html
[aurora-tls]: https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/UsingWithRDS.SSL.html
[aurora-audit]: https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Integrating.CloudWatch.html
[aurora-auth]: https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/UsingWithRDS.IAMDBAuth.html
[documentdb-tls]: https://docs.aws.amazon.com/documentdb/latest/developerguide/security.encryption.ssl.html
[documentdb-audit]: https://docs.aws.amazon.com/documentdb/latest/developerguide/event-auditing.html


* [DynamoDB](https://aws.amazon.com/dynamodb/)

* [RDS](https://aws.amazon.com/rds/)

* [Redshift](https://aws.amazon.com/redshift/)

* [Neptune](https://aws.amazon.com/neptune)

* [Aurora](https://aws.amazon.com/rds/aurora/)

* [DocumentDB](https://aws.amazon.com/documentdb/)

## Developer tools

* [Code Pipeline](https://aws.amazon.com/codepipeline/)

## End User Computing

* [WorkSpaces](https://aws.amazon.com/workspaces/)

## Management and Governance

* [CloudFormation](https://aws.amazon.com/cloudformation/)

* CloudWatch

* [**CloudTrail**](https://aws.amazon.com/cloudtrail/)

* [**Config**](https://aws.amazon.com/config/)

* [Control Tower](https://aws.amazon.com/controltower/)
 
* Management Console

* [Service Catalog](https://aws.amazon.com/servicecatalog/)

* [**Systems Manager (SSM)**](https://aws.amazon.com/systems-manager/)

* [**Trusted Advisor**](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/faqs/)

## Networking & Content Delivery

* [API Gateway](https://aws.amazon.com/api-gateway/)

* [CloudFront](https://aws.amazon.com/cloudfront/)

* [Route 53](https://aws.amazon.com/route53/)

* [Direct Connect](https://aws.amazon.com/directconnect/)

* [Transit Gateway](https://aws.amazon.com/transit-gateway/)

* [**VPC**](https://aws.amazon.com/vpc/)

## Storage

* [**S3**](https://aws.amazon.com/s3/)

* [Elastic Block Store (EBS)](https://aws.amazon.com/ebs/)

* [EFS](https://aws.amazon.com/efs/)

* [S3 Glacier](https://aws.amazon.com/glacier/)

* [Backup](https://aws.amazon.com/backup/)

* [Snow family](https://aws.amazon.com/snow/)
 
* [Storage Gateway](https://aws.amazon.com/storagegateway/)

