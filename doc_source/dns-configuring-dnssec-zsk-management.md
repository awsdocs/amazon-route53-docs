# KMS key and ZSK management in Route 53<a name="dns-configuring-dnssec-zsk-management"></a>

This section describes the current practice Route 53 uses for your DNSSEC signing enabled zones\.

**Note**  
Route 53 uses the following rule which might change\. Any future changes will not reduce your zone's or Route 53's security posture\.

**How Route 53 uses the AWS KMS associated with your KSK**  
In DNSSEC, the KSK is used to generate the resource record signature \(RRSIG\) for the DNSKEY resource record set\. All `ACTIVE` KSKs are used in the RRSIG generation\. Route 53 generates an RRSIG by calling the `Sign` AWS KMS API on the associated KMS key\. For more information, see [Sign](https://docs.aws.amazon.com/kms/latest/APIReference/API_Sign.html) in the *AWS KMS API guide*\. These RRSIGs do not count towards the zone’s resource record set limit\.  
RRSIG has an expiration\. To prevent the RRSIGs from expiring, the RRSIGs are refreshed regularly by regenerating them every one to seven days\.  
The RRSIGs are also refreshed every time you call any of these APIs:  
+ [ActivateKeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ActivateKeySigningKey.html)
+ [CreateKeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateKeySigningKey.html)
+ [DeactivateKeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeactivateKeySigningKey.html)
+ [DeleteKeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteKeySigningKey.html)
+ [DisableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DisableHostedZoneDNSSEC.html)
+ [EnableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_EnableHostedZoneDNSSEC.html)
Every time Route 53 performs a refresh, we generate 15 RRSIGs to cover the next few days in case the associated KMS key becomes inaccessible\. For KMS key cost estimation, you can assume a once a day regular refresh\. A KMS key might become inaccessible by inadvertent changes to the KMS key policy\. Inaccessible KMS key will set the associated KSK’s status to `ACTION_NEEDED`\. We strongly recommend that you monitor this condition by setting up a CloudWatch alarm whenever a `DNSSECKeySigningKeysNeedingAction` error is detected because validating resolvers will start failing lookups after the last RRSIG expires\. For more information, see [Monitoring hosted zones using Amazon CloudWatch](monitoring-hosted-zones-with-cloudwatch.md)\.

**How Route 53 manages your zone’s ZSK**  
Each new hosted zone with DNSSEC signing enabled will have one `ACTIVE` zone signing key \(ZSK\)\. The ZSK is generated separately for each hosted zone and is owned by Route 53\. The current key algorithm is ECDSAP256SHA256\.  
We will start performing regular ZSK rotation on the zone within 7–30 days of the start of signing\. Currently, Route 53 uses the Pre\-Publish Key Rollover method\. For more information, see [Pre\-Publish Zone Signing Key Rollover](https://datatracker.ietf.org/doc/html/rfc6781#section-4.1.1.1)\. This method will introduce another ZSK to the zone\. The rotation will be repeated every 7–30 days\.  
Route 53 will suspend ZSK rotation if any of the zone’s KSK is in `ACTION_NEEDED` status because Route 53 will not be able to regenerate the RRSIGs for DNSKEY resource record sets to account for the changes in the zone’s ZSK\. ZSK rotation will automatically resume after the condition is cleared\.