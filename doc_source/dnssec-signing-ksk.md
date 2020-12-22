# Key\-signing keys \(KSKs\)<a name="dnssec-signing-ksk"></a>

The key\-signing key \(KSK\) is a cryptographic public\-private key pair that signs the DNSKEY for DNSSEC signing\.

KSKs have one of the following statuses:
+ **Active** – The KSK is being used for signing\.
+ **Inactive** – The KSK is not being used for signing\.
+ **Internal Failure** – There was an error during a request\. Before you can continue to work with DNSSEC signing, including actions that involve this KSK, you must correct the problem\. For example, you might need to activate or deactivate the KSK\. 

Choose a KSK, then choose **View details**, or choose an option under **Action**\.

You can have up to two KSKs per hosted zone\.

## Learn more<a name="dnssec-signing-ksk-learn-more"></a>
+ [ Working with key\-signing keys \(KSKs\)](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-ksk.html)
+ [ Enabling DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)
+ [ Working with customer managed CMKs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-cmk-requirements.html)