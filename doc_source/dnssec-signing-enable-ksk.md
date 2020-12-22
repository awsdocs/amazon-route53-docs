# Key\-signing key \(KSK\)<a name="dnssec-signing-enable-ksk"></a>

Provide a name for the key\-signing key \(KSK\) that Route 53 will create for you automatically when you enable DNSSEC signing\. The KSK is a cryptographic public\-private key pair that signs the DNSKEY\. 

The KSK name that you provide can include numbers, letters, periods \(\.\), hyphens \(\-\), or underscores \(\_\)\. The name must be unique for each key\-signing key in the same hosted zone\.

The KSK is created based on a customer managed customer master key \(CMK\) in AWS KMS\.

The resulting signature is published, and resolvers can use it to validate against the corresponding plaintext DNSKEY with the public KSK\. During validation, a resolver ensures that the Delegation Signer \(DS\) record of the parent zone matches the corresponding DNSKEY record of this hosted zone, to authenticate the zone's key pair\.

You can have up to two KSKs per hosted zone\.

## Learn more<a name="dnssec-signing-enable-ksk-learn-more"></a>
+ [ Working with key\-signing keys \(KSKs\)](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-ksk.html)
+ [ Enabling DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)
+ [ Working with customer managed CMKs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-cmk-requirements.html)