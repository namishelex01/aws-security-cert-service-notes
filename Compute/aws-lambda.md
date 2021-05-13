* [**Lambda**](https://aws.amazon.com/lambda/)
    + Logs to CloudWatch
    + Execution role
        + assumed to run
        + at minimum CloudWatch logs creategroup/createstream/putevents
        + Potentially also XRay write, SQS/Kinesis/dynamodb read to get the event data
    + Resource policies
        + Resources: functions, their versions and aliases, and layer versions
            + `arn:aws:lambda:region:123456789012:function:my-function`
            + `arn:aws:lambda:region:123456789012:function:my-function:1`    - version
            + `arn:aws:lambda:region:123456789012:function:my-function:TEST` - alias
        + Use to give other services (principal: service: sns.ama...) and other accounts (principal: aws: account-arn) permission to use them
        + The console updates function policies automatically when you add a trigger to give the triggering service access
    * Identity policies
        + nice examples: ARN pattern so users have to include their username in function names; have to include a logging layer
        + To give users the ability to create functions with limited permissions, constrain what roles they can iam:PassRole on.
        + To give users the ability to add resource permissions to functions so they can be invoked, but only from specific sources, check lambda:Principal in a condition
    * VPC access
        + Can access resources in a VPC if subnet + security group is specified.
        + No internet access unless there is a NAT in the VPC.
        + No AWS service access unless there is internet access or VPC gateways
        + Role needs ability to create network interfaces in each subnet (and VPC must have ENI capacity & subnets must have spare IPs)
