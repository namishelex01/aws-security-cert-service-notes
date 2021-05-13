* [API Gateway](https://aws.amazon.com/api-gateway/)
    + Logs to CloudWatch
    + sigV4 signed requests with IAM; or Cognito User Pool token verification; or Lambda authorizers for other token verification
    + Can configure with a 'client-side' certificate that API gateway uses for authenticating its requests to backend servers
    + Resource based policies attached to API, the only action is `execute-api:Invoke`. Can use to allow cross-account access, or in combo with conditions to constrain access to specific VPCs / VPC endpoints / IP ranges etc. Rather complex [logic](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-authorization-flow.html) for evaluating them in combo with identity policies.
    + Supports rate limiting requests from an IP
    + Private APIs - only accessible through VPC endpoints.
    + Private integrations - connect to non-public VPC resources behind the API. Create an ELB network load balancer in the VPC, API Gateway associates it with a 'vpclink' VPC endpoint 
    + CORS - necessary to allow cross-origin requests; will need to be configured if using the default API gateway URLs rather than proxying via CloudFront, otherwise browsers won't honor requests to the API.
    + Integrates with WAF

