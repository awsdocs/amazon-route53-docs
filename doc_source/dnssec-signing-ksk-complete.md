# Establish a chain of trust<a name="dnssec-signing-ksk-complete"></a>

After you enable DNSSEC signing, you must establish a chain of trust for your hosted zone\.

Use the information about the key\-signing key \(KSK\) that Route 53 created for you to create a Delegation Signer \(DS\) record for the parent zone of your hosted zone\.

When your DNS update is complete and has propagated, resolvers can validate DNS responses from Route 53 for this hosted zone\.

## Learn more<a name="dnssec-signing-ksk-complete-learn-more"></a>
+ [ Establishing a chain of trust](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html#dns-configuring-dnssec-chain-of-trust)
+ [ Enabling DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)