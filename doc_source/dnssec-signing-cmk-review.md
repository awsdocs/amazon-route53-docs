# Update customer managed CMK permissions<a name="dnssec-signing-cmk-review"></a>

The customer managed customer master key \(CMK\) that you specify when Route 53 creates a key\-signing key \(KSK\) for you must have the required permissions to use the key for DNSSEC signing\.

Update your customer managed CMK to allow Route 53 to do the following: DescribeKey, GetPublicKey, and Sign\.

Alternatively, you can create and use another customer managed CMK for DNSSEC signing that has the required permissions\.

## Learn more<a name="dnssec-signing-cmk-review-learn-more"></a>
+ [ Working with customer managed CMKs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-cmk-requirements.html)
+ [DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec.html)
+ [ KMS key policy for DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/access-control-managing-permissions.html#KMS-key-policy-for-DNSSEC)