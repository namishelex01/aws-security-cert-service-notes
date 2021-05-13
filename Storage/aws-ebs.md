# AWS EBS

Redundancy but only within a single AZ
Snapshots might be useful for recovery
Encryption (if enabled) happens on the EC2 server side (outside the EC2 VM), hence encrypted in transit and rest. Uses KMS - wrapped data key stored alongside volume.
ec2:CreateVolume action paired with ec2:Encrypted condition key can enforce use of encrypted volumes
