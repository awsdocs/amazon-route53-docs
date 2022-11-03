# Configuring DNSSEC signing in Amazon Route 53<a name="dns-configuring-dnssec"></a>

Domain Name System Security Extensions \(DNSSEC\) signing lets DNS resolvers validate that a DNS response came from Amazon Route 53 and has not been tampered with\. When you use DNSSEC signing, every response for a hosted zone is signed using public key cryptography\.

In this chapter, we explain how to enable DNSSEC signing for Route 53, how to work with key\-signing keys \(KSKs\), and how to troubleshoot issues\. You can work with DNSSEC signing in the AWS Management Console or programmatically with the API\. For more information about using the CLI or SDKs to work with Route 53, see [Setting up Amazon Route 53](setting-up-route-53.md)\.

Before you enable DNSSEC signing, note the following:
+ To help prevent a zone outage and avoid problems with your domain becoming unavailable, you must quickly address and resolve DNSSEC errors\. We strongly recommend that you set up a CloudWatch alarm that alerts you whenever a `DNSSECInternalFailure` or `DNSSECKeySigningKeysNeedingAction` error is detected\. For more information, see [Monitoring hosted zones using Amazon CloudWatch](monitoring-hosted-zones-with-cloudwatch.md)\.
+ There are two kinds of keys in DNSSEC: a key\-signing key \(KSK\) and a zone\-signing key \(ZSK\)\. In Route 53 DNSSEC signing, each KSK is based on an [asymmetric customer managed key](https://docs.aws.amazon.com/kms/latest/developerguide/symm-asymm-concepts.html#asymmetric-cmks) in AWS KMS that you own\. You are responsible for KSK management, which includes rotating it if needed\. ZSK management is performed by Route 53\.
+ When you enable DNSSEC signing for a hosted zone, Route 53 limits the TTL to one week\. If you set a TTL of more than one week for records in the hosted zone, you don't get an error\. However, Route 53 enforces a TTL of one week for the records\. Records that have a TTL of less than one week and records in other hosted zones that do not have DNSSEC signing enabled are not affected\. 
+ When you use DNSSEC signing, multi\-vendor configurations are not supported\. If you have configured white\-label name servers \(also known as vanity name servers or private name servers\), make sure those name servers are provided by a single DNS provider\.
+ Some DNS providers do not support Delegation Signer \(DS\) records in their authoritative DNS\. If your parent zone is hosted by a DNS provider who does not support DS queries \(not setting AA flag in the DS query response\), then when you enable DNSSEC in its child zone, the child zone will become unresolvable\. Make sure your DNS provider supports DS records\.
+ It can be helpful to set up IAM permissions to allow another user, besides the zone owner, to add or remove records in the zone\. For example, a zone owner can add a KSK and enable signing, and might also be responsible for key rotation\. However, someone else might be responsible for working with other records for the hosted zone\. For an example IAM policy, see [Example permissions for a domain record owner](access-control-managing-permissions.md#example-permissions-record-owner)\.

**Topics**
+ [Enabling DNSSEC signing and establishing a chain of trust](dns-configuring-dnssec-enable-signing.md)
+ [Disabling DNSSEC signing](dns-configuring-dnssec-disable.md)
+ [Working with customer managed keys for DNSSEC](dns-configuring-dnssec-cmk-requirements.md)
+ [Working with key\-signing keys \(KSKs\)](dns-configuring-dnssec-ksk.md)
+ [KMS key and ZSK management in Route 53](dns-configuring-dnssec-zsk-management.md)
+ [DNSSEC proofs of nonexistence in Route 53](dns-configuring-dnssec-proof-of-nonexistence.md)
+ [Troubleshooting DNSSEC signing](dns-configuring-dnssec-troubleshoot.md)