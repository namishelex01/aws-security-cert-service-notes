# AWS ECS

Tasks: set of containers that are placed together.
Containers run on customer-controlled EC2 instances in a VPC, or are Fargate managed.
Networking options:
none
bridge - docker's virtual network
host - tasks get the host's network interface
awsvpc: Task network interfaces are normal ENIs so all the VPC properties apply: exist in a subnet, have security groups, have flow logs. Also means each container can have its own security group & IP, vs host networking where all the containers on one host share interfaces.
Tasks are configured with an execution role they use to access services
Can send logs to CloudWatch
Fargate launch type
Must use awsvpc network mode, CloudWatch logs
Uses Firecracker under the hood (definitely not in scope of the exam, but an interesting topic!)
