# DS record<a name="dnssec-signing-ds-record"></a>

To complete setting up DNSSEC signing for a hosted zone, you establish a chain of trust for your hosted zone by creating a Delegation Signer \(DS\) record in the parent zone\.

If your hosted zone is with Route 53, choose that option and use the provided information to create a DS record in the parent zone\.

If your hosted zone is with another domain registrar, choose that option and use the provided information to create a record for DNSSEC signing at the registrar\. Follow the guidance provided by your registrar to create a DS record or otherwise update the parent zone correctly for DNSSEC signing\.

## Learn more<a name="dnssec-signing-ds-record-learn-more"></a>
+ [ Establishing a chain of trust](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html#dns-configuring-dnssec-chain-of-trust)
+ [ Enabling DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)