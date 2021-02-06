# Working with key\-signing keys \(KSKs\)<a name="dns-configuring-dnssec-ksk"></a>

When you enable DNSSEC signing, Route 53 creates a key\-signing key \(KSK\) for you\. You can have up to two KSKs in Route 53\. After you enable DNSSEC signing, you can add, remove, or edit your KSKs\.

Note the following when you work with your KSKs:
+ Before you can delete a KSK, you must edit the KSK to set its status to **Inactive**\. 
+ When DNSSEC signing is enabled for a hosted zone, Route 53 limits the TTL to one week\. If you set a TTL for records in the hosted zone to more than one week, you don't get an error, but Route 53 enforces a TTL of one week\.
+ To help prevent a zone outage and avoid problems with your domain becoming unavailable, you must quickly address and resolve DNSSEC errors\. We strongly recommend that you set up a CloudWatch alarm that alerts you whenever a `DNSSECInternalFailure` or `DNSSECKeySigningKeysNeedingAction` error is detected\. For more information, see [Monitoring hosted zones using Amazon CloudWatch](monitoring-hosted-zones-with-cloudwatch.md)\.
+ The KSK operations described in this section allow you to rotate your zone’s KSKs\. For more information and a step\-by\-step example, see *DNSSEC Key Rotation* in the blog post [ Configuring DNSSEC signing and validation with Amazon Route 53](https://aws.amazon.com/blogs/networking-and-content-delivery/configuring-dnssec-signing-and-validation-with-amazon-route-53/)\.

To work with KSKs in the AWS Management Console, follow the guidance in the following sections\.

## Add a key\-signing key \(KSK\)<a name="dns-configuring-dnssec-ksk-add-ksk"></a>

When you enable DNSSEC signing, Route 53 creates a key\-signing \(KSK\) for you\. You can also add KSKs separately\. You can have up to two KSKs in Route 53\. 

When you create a KSK, you must provide or request Route 53 to create a customer managed CMK to use with the KSK\. When you provide or create a customer managed CMK, there are several requirements\. For more information, see [Working with customer managed CMKs for DNSSEC](dns-configuring-dnssec-cmk-requirements.md)\.

Follow these steps to add a KSK in the AWS Management Console\.<a name="dns-configuring-dnssec-ksk-add-ksk-procedure"></a>

**To add a KSK**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone\.

1. On the **DNSSEC signing** tab, under **Key\-signing keys \(KSKs\)** under **Actions**, choose **Add KSK**\.

1. Under **KSK**, enter a name for the KSK that Route 53 will create for you\. The name can include numbers, letters, and underscores \(\_\)\. It must be unique\.

1. Enter the alias for a customer managed CMK that applies to DNSSEC signing, or enter an alias for a new customer managed CMK that Route 53 will create for you\.
**Note**  
If you choose to have Route 53 create a customer managed CMK, be aware that separate charges apply for each customer managed CMK\. For more information, see [AWS Key Management Service pricing](https://aws.amazon.com/kms/pricing/)\.

1. Choose **Create KSK**\.

## Edit a key\-signing key \(KSK\)<a name="dns-configuring-dnssec-ksk-edit-ksk"></a>

You can edit the status of a KSK to be **Active** or **Inactive**\. When a KSK is active, Route 53 uses that KSK for DNSSEC signing\. Before you can delete a KSK, you must edit the KSK to set its status to **Inactive**\.

Follow these steps to edit a KSK in the AWS Management Console\.<a name="dns-configuring-dnssec-ksk-edit-ksk-procedure"></a>

**To edit a KSK**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone\.

1. On the **DNSSEC signing** tab, under **Key\-signing keys \(KSKs\)** under **Actions**, choose **Edit KSK**\.

1. Make the desired updates to the KSK, and then choose **Save**\.

## Delete a key\-signing key \(KSK\)<a name="dns-configuring-dnssec-ksk-delete-ksk"></a>

Before you can delete a KSK, you must edit the KSK to set its status to **Inactive**\. 

One reason that you might delete a KSK is as part of routine key rotation\. It's a best practice to rotate cryptographic keys periodically\. Your organization might have standard guidance for how often to rotate keys\. 

Follow these steps to delete a KSK in the AWS Management Console\.<a name="dns-configuring-dnssec-ksk-delete-ksk-procedure"></a>

**To delete a KSK**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone\.

1. On the **DNSSEC signing** tab, under **Key\-signing keys \(KSKs\)** under **Actions**, choose **Delete KSK**\.

1. Follow the guidance to confirm deleting the KSK\.