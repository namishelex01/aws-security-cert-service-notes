# AWS Service Catalog

Portfolio: collection of catalogs. Catalogs: collection of products. Product: CloudFormation template (with the usual optional CloudFormation parameters).
Portfolios can be shared across accounts.
Admin access control is via IAM. User access control is initially via IAM - You need ServiceCatalogEndUserAccess to use Service Catalog. It doesn't support resource-level permissions nor resource-based policies, which is weird. Portfolio access is instead managed within Service Catalog by associating IAM users/groups/roles with a Portfolio.
Launch role: a role that is used to run the templates, instead of the user having the necessary permissions. Don't think the user needs iam:PassRole to use it - so a way of constraining user of the permissions in the role.
