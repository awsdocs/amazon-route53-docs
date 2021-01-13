# Enable DNSSEC signing<a name="dnssec-signing-enable"></a>

When you enable DNSSEC signing, Route 53 automatically creates a key\-signing key \(KSK\) for you, based on the customer managed customer master key \(CMK\) in AWS Key Management Service \(AWS KMS\) that you choose\.

Choose a name for the KSK, then decide whether to use an existing customer managed CMK that applies to DNSSEC signing, or have Route 53 create a new one for you\.

After you enable DNSSEC signing, complete DNSSEC signing setup by establishing a chain of trust\. You do this by creating a Delegation Signer \(DS\) record for the parent zone of this zone\. When that DNS update is complete and has propagated, resolvers can validate DNS responses from Route 53 for this hosted zone\.

## Learn more<a name="dnssec-signing-enable-learn-more"></a>
+ [DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec.html)
+ [ Enabling DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)
+ [Establishing a chain of trust](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html#dns-configuring-dnssec-chain-of-trust)