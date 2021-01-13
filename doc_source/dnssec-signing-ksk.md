# Key\-signing keys \(KSKs\)<a name="dnssec-signing-ksk"></a>

The key\-signing key \(KSK\) is a cryptographic public\-private key pair that signs the DNSKEY for DNSSEC signing\. You can have up to two KSKs per hosted zone\.

Choose a KSK, then choose **View details**, or choose an option under **Action**\.

KSKs have one of the following statuses:
+ **Active** – The KSK is being used for signing\.
+ **Inactive** – The KSK is not being used for signing\.
+ **Internal Failure** – There was an error during a request\. Before you can continue to work with DNSSEC signing, including actions that involve this KSK, you must correct the problem\. For example, you might need to activate or deactivate the KSK\. 

To help prevent a zone outage and avoid problems with your domain becoming unavailable, you must quickly address and resolve DNSSEC errors\. We strongly recommend that you set up a CloudWatch alarm that alerts you whenever a `DNSSECInternalFailure` or `DNSSECKeySigningKeysNeedingAction` error is detected\. For more information, see [Monitoring hosted zones using Amazon CloudWatch](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/monitoring-hosted-zones-with-cloudwatch.html)\.

## Learn more<a name="dnssec-signing-ksk-learn-more"></a>
+ [ Working with key\-signing keys \(KSKs\)](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-ksk.html)
+ [ Enabling DNSSEC signing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)
+ [ Working with customer managed CMKs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-cmk-requirements.html)