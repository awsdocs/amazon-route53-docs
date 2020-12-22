# Customer managed CMK<a name="dnssec-signing-enable-cmk"></a>

Route 53 creates a key\-signing key \(KSK\) for DNSSEC signing based on a customer managed customer master key \(CMK\) in AWS Key Management Service \(AWS KMS\)\.

If you already have a customer managed CMK that applies to DNSSEC signing, you can choose that option and then specify the ARN for the key\.

Alternatively, you can create a new customer managed CMK to use for DNSSEC signing\. Provide an alias for the new key, and Route 53 will create it for you automatically in AWS KMS when you choose **Create KSK and enable signing**\.

## Learn more<a name="dnssec-signing-enable-cmk-learn-more"></a>
+ [ Working with customer managed CMKs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-cmk-requirements.html)
+ [DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dnssec-signing.html)
+ [ KMS key policy for DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/access-control-managing-permissions.html#KMS-key-policy-for-DNSSEC)