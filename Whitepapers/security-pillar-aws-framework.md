# Security Pillar - AWS Framework

## Security Foundation

### Design Principles

  + Implement a strong identity foundation
  + Enable traceability
  + Apply security at all layers
  + Automate security best practices
  + Protect data in transit and at rest
  + Keep people away from data
  + Prepare for security events

### Security in Cloud

  + IAM
  + Detection
  + Infra Protection
  + Data Protection
  + Incident Response

### AWS Account Management and Separation

  + Separate workloads using accounts: 
    + Account-level separation is strongly recommended for isolating production environments from development and test environments, or providing a strong logical boundary between workloads that process data of different sensitivity levels, as defined by external compliance requirements (such as PCI-DSS or HIPAA), and workloads that don’t.

  + Secure AWS account: 
    + Not using the root user
    + Use AWS Organizations to centrally manage and govern your accounts as you grow and scale your workloads in AWS. AWS Organizations helps you manage accounts, set controls, and configure services across your accounts.

  + Manage accounts centrally: 
    + AWS Organizations automates AWS account creation and management, and control of those accounts after they are created. When you create an account through AWS Organizations, it is important to consider the email address you use, as this will be the root user that allows the password to be reset. 
    + Organizations allows you to group accounts into organizational units(OUs), which can represent different environments based on the workload’s requirements and purpose.
  + Set controls centrally:
    + AWS Organizations allows you to use service control policies (SCPs) to apply permission guardrails at the organization, organizational unit, or account level, which apply to all AWS Identity and Access Management (IAM) users and roles. 
    + AWS Control Tower offers a simplified way to set up and govern multiple accounts. It automates the setup of accounts in your AWS Organization, automates provisioning, applies guardrails (which include prevention and detection), and provides you with a dashboard for visibility.
  + Configure services and resources centrally: 
    + AWS Organizations helps you configure AWS services that apply to all of your accounts. 
    + For example, you can configure central logging of all actions performed across your organization using AWS CloudTrail, and prevent member accounts from disabling logging.
    + You can also centrally aggregate data for rules that you’ve defined using AWS Config, enabling you to audit your workloads for compliance and react quickly to changes. 
    + AWS CloudFormation StackSets allow you to centrally manage AWS CloudFormation stacks across accounts and OUs in your organization. This allows you to automatically provision a new account to meet your security requirements

### IAM

### Detection

### Infra Protection

### Data Protection

### Incident Response

