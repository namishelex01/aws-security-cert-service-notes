# AWS CloudFront

Optional access logs to S3 - bucket ACL configured to give the awslogsdelivery account full control. Metrics via CloudWatch.
Field level encryption - CloudFront can encrypt specific POST fields with a public key you've configured. Reduces exposure of sensitive data as it passes through the backend.
HTTPS: can configure HTTP, redirect to HTTPS, or HTTPS only for client side. For origin side can do HTTP, match viewer, or HTTPS.
To serve content from S3 only via CloudFront, create an 'origin access identity' for the distribution, then create a bucket policy that blocks public access and allows the special "Principal":{"CanonicalUser":"<CloudFront Origin Identity Canonical User ID>"}
Can only allow specific geographic regions based on IP
Can require signed URLs or signed Cookies - CloudFront creates keypairs for each "trusted signer" AWS account, and the account generates time-limited signed URLs or Cookies for clients to use.
