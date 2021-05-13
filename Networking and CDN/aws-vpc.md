# AWS VPC

Spans all AZs in a single region
Soft limit of 5 VPCs per region
Has a CIDR, can have 4 additional CIDRs
See example scenarios
Policy resources and condition keys
Most resources support the ec2:Vpc and ec2:Region condition keys. Other notable ones listed below.
arn:aws:ec2:<region>:<account>:internet-gateway/igw-id
arn:aws:ec2:<region>:<account>:network-acl/nacl-id
arn:aws:ec2:<region>:<account>:network-interface/eni-id and ec2:{Subnet,AvailabilityZone}
arn:aws:ec2:<region>:<account>:route-table/route-table-id
arn:aws:ec2:<region>:<account>:security-group/security-group-id
arn:aws:ec2:<region>:<account>:vpc/vpc-id and ec2:Tenancy
Network interfaces
Has one or more IP addresses, a MAC address, one or more security groups,
Can be moved between EC2 instances
Can't move the primary interface of an instance
Egress options:
Internet Gateway
Attached to VPC
Interface must have a public address, but the gateway does NAT so incoming traffic is addressed to the interface's private address
Virtual Private Gateway
IPSec VPN attached to a VPC
Need a corresponding customer gateway in the other network(s)
Route table(s) need updating to point at customer gateway. Route propagation can do this automatically.
Security groups need rules to allow access from remote network
VPC Peering Connection
VPC peering can cross both accounts and regions, but is not transitive between VPCs
VPC Endpoints
To keep service traffic within AWS. No public IP needed.
Endpoint policies - resource policies that constrain what service actions are possible via that endpoint.
S3 bucket policies can limit access to a specific endpoint or VPC using aws:sourceVpce and aws:sourceVpc, e.g.:
{   "Sid": "specific-vpc-endpoint",
    "Condition": {
        "StringNotEquals": {
            "aws:sourceVpce": "vpce-1a2b3c4d"
        }
    },
Similarly can use aws:sourceVpce in an identity policy for DynamoDB
Gateway Endpoint
Gateway in the VPC that you route to with a special-case entry in route tables
S3 and DynamoDB only - they don't have interface endpoints
Interface Endpoint (PrivateLink)
Elastic network interface with a private IP address
In a subnet and security group(s) - security group needs to allow outbound access to the service
Several services including EC2, ELB, SNS, CloudWatch, Systems Manager, and various Marketplace products.
Has an endpoint specific DNS hostname.
Private DNS allows you to use the normal hostname for the services, by creating a DNS zone in the VPC using Route53 that has a record for the service that resolves to the interface's private IP address.
NAT Gateway
To prevent unsolicited inbound connections but allow outbound connections for instances without a public IP
Within a public subnet, in a specific AZ
The subnet's NACL applies, but NAT Gateways aren't in any security groups
Has an Elastic IP address
Connects to an Internet Gateway
Can be used by instances in a different (private) subnet in the same VPC
Also see Transit Gateway
Subnets
Within a single AZ
Can be shared across accounts!
CIDR is within the VPC's CIDR and can't overlap other subnets in the VPC. Must have IPv4 CIDR.
Associated with a route table for outbound traffic. Default to VPC's main route table.
Public subnet = route table includes an internet gateway. Otherwise called a private subnet.
Instances have a private IP and optionally (configured at subnet + instance level) either a public IP (random from AWS' pool) or an Elastic IP (persistent, owned by your account)
Instances with a public/elastic IP also get a public DNS hostname
Network ACLs
Each subnet has a NACL
What traffic can enter/exit a subnet
Stateless - must have explicit inbound and outbound rules - replies aren't special. For web-facing servers, need to allow outbound ephemeral ports e.g. 1024+ for all addresses
VPC default NACL is used for new subnets, its initial rules allow all traffic
Rules: Allow/Deny, dest port, src/dst addr, protocol.
Rules evaluated in order until one matches. Default deny (there's an immutable final deny rule that matches all).
Custom NACLs start with no rules (except the deny-all).
Route tables
Exist in the VPC. Subnets are associated with a single route table
The most specific route that matches is used
Always have unmodifiable local routes for in-VPC traffic
Need to have entries for gateways and VPC peering
New VPCs have a main route table. You can make a custom route table the main one.
Flow logs
to S3 or CloudWatch Logs
Log streams/files are per interface, but can be configured at VPC, subnet, or network interface level
Capture window: ~10 minutes after which a log entry is published
<version> <account-id> <interface-id> <srcaddr> <dstaddr> <srcport> <dstport> <protocol> <packets> <bytes> <start> <end> <action> <log-status>
Doesn't record: Amazon DNS requests (does record requests to a custom DNS server); 169.254.169.254 metadata; DHCP; traffic to the default VPC router
Identity policies only - no resource based policies
Flow logs service needs a role to assume so it can publish logs to S3 or CloudWatch, and users need iam:PassRole for the role
S3 Bucket policy must allow the service to PutObject + a bit more. Automatically created if the flow log creator can create and modify bucket policies.
Security groups
What traffic can flow to/from an instance
Allow rules only, direction specific.
Multiple SGs per instance are possible.
Rules on src/dest, dest port, protocol (TCP, UDP, etc)
src/dest can be ip range; a sg in this VPC or a peered one; service prefix list for gateway endpoints
Default rules in a new group: no inbound, all outbound.
The default security group also allows inbound from other instances in the sg.
Stateful - responses are always allowed
Can reference SGs in peered VPCs.
