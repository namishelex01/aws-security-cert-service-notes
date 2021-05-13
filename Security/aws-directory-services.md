* [**Directory Service**](https://aws.amazon.com/directoryservice/faqs/)
    + Works with EC2 (manage them via group policies), RDS SQL server, WorkSpaces, AWS SSO, and a few more obscure ones
    + Can assign IAM roles to AD users for AWS access
    * Managed Microsoft AD
        + Can join to existing AD with trust relationships
        + Or replace an on-prem AD by using Direct Connect or VPN
        + EBS volumes are encrypted. Deployed on two AZs. Daily backups.
        + Some high-priv operations not available. No remote access or powershell access. You get an OU and delegated admin account for it.
    * AD Connector
        + Proxy for [a specific list of AWS services](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ad_connector_app_compatibility.html) through to on-prem AD.
        + Notably works with: SSO; management console; EC2 Windows (join domain)
    * Simple AD
        + Samba backend. Like Managed Microsoft AD but less features and smaller resource limits.

