# Troubleshooting DNSSEC signing<a name="dns-configuring-dnssec-troubleshoot"></a>

The information in this section can help you address issues with DNSSEC signing, including with your key\-signing keys \(KSKs\)\.

KSK status is **Action needed**  
If the status for a KSK is **Action needed**, you must fix the customer managed customer master key \(CMK\) that the KSK is based on\. For example, the permissions might have been changed for the customer managed CMK, or the customer managed CMK might have been removed\.  
To correct the problem, make sure that the customer managed CMK that your KSK is based on has the correct permissions\. For more information, see [Route 53 CMK permissions required for DNSSEC signing](access-control-managing-permissions.md#KMS-key-policy-for-DNSSEC)\.

KSK status is **Internal failure**  
When a KSK has a status of **Internal failure**, you can't work with any other DNSSEC entities until the problem is resolved\. You must take action before you can work with DNSSEC signing, including working with this KSK or your other KSK\.  
To correct the problem, try again to activate or deactivate the KSK\.  
If you're working with the Route 53 API, you might also see a DNSSEC signing status of `INTERNAL_FAILURE`\. To correct the problem, try enabling signing \([EnableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_EnableHostedZoneDNSSEC.html)\) or disabling signing \([ DisableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DisableHostedZoneDNSSEC.html)\)\.  
It's important that you correct **Internal failure** problems promptly\. You can't make any other changes to the hosted zone until you correct the problem, except the operations to fix the **Internal failure**\.