# Troubleshooting DNSSEC signing<a name="dns-configuring-dnssec-troubleshoot"></a>

The information in this section can help you address issues with DNSSEC signing, including with your key\-signing keys \(KSKs\)\.

KSK status is **Action needed**  
A KSK can change its status to **Action needed** \(or `ACTION_NEEDED` in a [KeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_KeySigningKey.html) status\), when Route 53 DNSSEC loses access to a corresponding AWS KMS key \(due to a change in permissions or AWS KMS key deletion\)\.  
If the status of a KSK is **Action needed**, it means that eventually it'll cause a zone outage for clients using DNSSEC validating resolvers and you must act fast to prevent a production zone becoming un\-resolvable\.  
To correct the problem, make sure that the customer managed key that your KSK is based on is enabled and has the correct permissions\. For more information about the required permissions, see [Route 53 customer managed key permissions required for DNSSEC signing](access-control-managing-permissions.md#KMS-key-policy-for-DNSSEC)\.  
After you have fixed the KSK, activate it again by using the console or the AWS CLI, as described in [Step 2: Enable DNSSEC signing and create a KSK](dns-configuring-dnssec-enable-signing.md#dns-configuring-dnssec-enable)\.  
To prevent this issue in the future, consider adding an Amazon CloudWatch metric to track the state of the KSK as suggested in [Configuring DNSSEC signing in Amazon Route 53](dns-configuring-dnssec.md)\.

KSK status is **Internal failure**  
When a KSK has a status of **Internal failure** \(or `INTERNAL_FAILURE` in a [KeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_KeySigningKey.html) status\), you can't work with any other DNSSEC entities until the problem is resolved\. You must take action before you can work with DNSSEC signing, including working with this KSK or your other KSK\.  
To correct the problem, try again to activate or deactivate the KSK\.  
 To correct the problem when working with the APIs, try enabling signing \([EnableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_EnableHostedZoneDNSSEC.html)\) or disabling signing \([ DisableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DisableHostedZoneDNSSEC.html)\)\.  
It's important that you correct **Internal failure** problems promptly\. You can't make any other changes to the hosted zone until you correct the problem, except the operations to fix the **Internal failure**\.