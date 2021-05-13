# AWS ELB

Integrated with Certificate Manager to terminate TLS. Can also upload certs to IAM and configure ELB to use them from there.
Can specify which of several predefined cipher-suites - 'security policies' - to support
Application Load Balancer (ALB) - HTTP/HTTPS
In a security group
Integrated with WAF
Authentication: integrates with Cognito and supports Open ID Connect. Redirects users to IdP authorization endpoint, then adds headers with signed JWT containing user info.
Can have a Lambda function as a target. Transforms JSON response to HTTP. Function policy needs to allow elasticloadbalancing.amazonaws.com to InvokeFunction
Can enable access logging to an S3 bucket
Network Load Balancer - TCP/TLS
Doesn't support Server Name Indication (SNI)
2k RSA certs only (ALB is more flexible)
Creates a (read only) network interface in a subnet in each AZ you choose. Not in a security group - instance security groups must allow traffic from its IP address and from client IP addresses
(Classic)
Logs to S3
