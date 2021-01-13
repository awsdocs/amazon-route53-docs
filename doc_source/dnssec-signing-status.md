# DNSSEC signing status<a name="dnssec-signing-status"></a>

DNSSEC signing lets DNS resolvers validate that a DNS response has not been tampered with\. When you use DNSSEC signing, every record in a Route 53 hosted zone is signed using public key cryptography\.

To set up DNSSEC signing, you must enable it and have Route 53 create a key\-signing key \(KSK\)\. Then you complete the process by creating a Delegation Signer \(DS\) record for the parent zone of the zone\. This creates the required chain of trust for the hosted zone\.

## Learn more<a name="dnssec-signing-status-learn-more"></a>
+ [DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec.html)
+ [ Enabling DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)
+ [ KMS key policy for DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/access-control-managing-permissions.html#KMS-key-policy-for-DNSSEC)