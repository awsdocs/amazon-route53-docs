# Follow DNSSEC signing enabling steps in order<a name="dnssec-signing-enable-steps"></a>

To set up DNSSEC signing, do the following:

1. Complete the steps on this page, to enable DNSSEC signing and have Route 53 create a KSK for you\. 

1. Next, finish DNSSEC signing setup by establishing a chain of trust for your hosted zone\. You do this by creating a Delegation Signer \(DS\) record for the parent hosted zone\. 

The KSK is a cryptographic public\-private key pair that signs the DNSKEY\. The KSK name that you provide can include numbers, letters, periods \(\.\), hyphens \(\-\), or underscores \(\_\)\. The name must be unique for each key\-signing key in the same hosted zone\.

You must follow these steps in order\. If you don't, your domain might become unavailable on the internet\.

## Learn more<a name="dnssec-signing-enable-steps-learn-more"></a>
+ [DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dnssec-signing.html)
+ [ Enabling DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)