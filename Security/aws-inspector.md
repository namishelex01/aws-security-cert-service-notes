* [Inspector](https://aws.amazon.com/inspector/faqs/)
    * Rules packages
        + Predefined only.
        + Network: Network Reachability
        + Host: CVEs; CIS Benchmarks; Security Best Practices (OS config incl remote access); Runtime Behavior Analysis (protocols, ports, software config)
    * Template
        + Rules packages (predefined only), target EC2 instances, SNS topic
    + Network reachability + host config (CVEs in package manager installed software, CIS benchmarks for popular OSes)
    * Agent required for host config
    + Network reachability: enumerates what ports are accessible from outside of a VPC (+ what process listening on those ports, with agents)
    + Service linked role to enumerate EC2 instances and network config
    + Simple schedule in template, or more advanced via CloudWatch events / custom use of API

