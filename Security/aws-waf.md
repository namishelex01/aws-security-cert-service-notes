* [WAF](https://aws.amazon.com/waf/faqs/)
    * Conditions
        + Inspect: IP addresses (+ region mapping), HTTP headers, HTTP body, URI strings
        + Match against: SQL injection, cross-site scripting, regex, strings, IP ranges, regions, sizes.
    * Rules
        + Comprise a number of conditions ANDed together
        + Rate based rule - 5 minute period for given IP, e.g. to protect against DDoS or login brute forcing
        + Need conditions for normal rules, but they're optional for rate-based rules (no condition=all requests count)
        + Managed rules from Marketplace sellers.
    * Web ACLs
        + Collection of rules, ORed together
        + Actions per rule: allow, block, or count (for testing)
        + Default action if no rule matches
    + Associate Web ACLs with CloudFront, ALB, and API Gateway instances which will then proxy requests via WAF and act on result
    + Also see Firewall Manager and Shield (Advanced)
