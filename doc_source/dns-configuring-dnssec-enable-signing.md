# Enabling DNSSEC signing and establishing a chain of trust<a name="dns-configuring-dnssec-enable-signing"></a>

This section provides step\-by\-step information for enabling and disabling DNSSEC signing in the Amazon Route 53 console\. There are two steps to enabling DNSSEC signing: enabling signing and having Route 53 create a key\-signing key \(KSK\), and establishing a chain of trust\.

To enable DNSSEC signing programmatically, see [Using the AWS CLI to enable DNSSEC signing](dns-configuring-dnssec-cli.md)\.

**Topics**
+ [Enabling DNSSEC signing and creating a KSK](#dns-configuring-dnssec-enable)
+ [Establishing a chain of trust](#dns-configuring-dnssec-chain-of-trust)
+ [Enabling DNSSEC signing with an existing KSK](#dns-configuring-dnssec-enable-existing-ksk)

## Enabling DNSSEC signing and creating a KSK<a name="dns-configuring-dnssec-enable"></a>

To get started using DNSSEC signing in Route 53, you enable DNSSEC signing, and then Route 53 creates a key\-signing key \(KSK\) for you, based on a customer managed customer master key \(CMK\) that you choose\. 

When you provide or create a customer managed CMK, there are several requirements\. For more information, see [Working with customer managed CMKs for DNSSEC](dns-configuring-dnssec-cmk-requirements.md)\.<a name="dns-configuring-dnssec-enable-procedure"></a>

**To enable DNSSEC signing and create a KSK**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone that you want to enable DNSSEC signing for\.

1. On the **DNSSEC signing** tab, choose **Enable DNSSEC signing**\.
**Note**  
If the option in this section is **Disable DNSSEC signing**, you have already completed the first step in enabling DNSSEC signing\. Be sure that you establish, or that there already exists, a chain of trust for the hosted zone for DNSSEC, and then you're done\. For more information, see [Establishing a chain of trust](#dns-configuring-dnssec-chain-of-trust)\.

1. Under **KSK**, enter a name for the KSK that Route 53 will create for you\. The name can include numbers, letters, and underscores \(\_\)\. It must be unique\.

1. Under **Customer managed CMK**, choose the customer managed CMK for Route 53 to use when it creates the KSK for you\. You can use an existing customer managed CMK that applies to DNSSEC signing, or create a new customer managed CMK\.

   When you provide or create a customer managed CMK, there are several requirements\. For more information, see [Working with customer managed CMKs for DNSSEC](dns-configuring-dnssec-cmk-requirements.md)\.

1. Enter the alias for an existing customer managed CMK\. If you want to use a new customer managed CMK, enter an alias for a customer managed CMK, and Route 53 will create one for you\.
**Note**  
If you choose to have Route 53 create a customer managed CMK, be aware that separate charges apply for each customer managed CMK\. For more information, see [AWS Key Management Service pricing](https://aws.amazon.com/kms/pricing/)\.

1. Choose **Enable DNSSEC signing**\.

## Establishing a chain of trust<a name="dns-configuring-dnssec-chain-of-trust"></a>

After you enable DNSSEC signing for a hosted zone in Route 53, establish a chain of trust for the hosted zone to complete your DNSSEC signing setup\. You do this by creating a Delegation Signer \(DS\) record in the *parent* hosted zone, for your hosted zone, using the information that Route 53 provides\. Depending on where your domain is registered, you add the record to the parent hosted zone in Route 53 or at another domain registrar\.<a name="dns-configuring-dnssec-chain-of-trust-procedure"></a>

**To establish a chain of trust for DNSSEC signing**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone that you want to establish a DNSSEC chain of trust for\. *You must enable DNSSEC signing first\.*

1. On the **DNSSEC signing** tab, under **DNSSEC signing**, choose **View information to create DS record**\.
**Note**  
If you don't see **View information to create DS record** in this section, then you must enable DNSSEC signing before you establish the chain of trust\. Choose **Enable DNSSEC signing** and complete the steps, and then return to these steps to establish the chain of trust\.

1. Under **Establish a chain of trust**, choose either **Route 53 registrar** or **Another domain registrar**, depending on where your domain is registered\.

1. Use the provided values to create a DS record for the parent hosted zone in Route 53 or, if your domain is not hosted at Route 53, use the provided values to create a DS record at your domain registrar website\. 

   Make sure you that configure the correct signing algorithm \(ECDSAP256SHA256 and type 13\) and digest algorithm \(SHA\-265 and type 2\)\. 

   If Route 53 is your registrar:

   1. Note the **Key type**, **Signing algorithm**, and **Public key** values\. In the navigation pane, choose **Registered domains**\.

   1. Select a domain, and then, next to **DNSSEC status**, choose **Manage keys**\.

   1. In the **Manage DNSSEC keys** dialog, choose the appropriate **Key type** and **Algorithm** for the **Route 53 registrar** from the dropdown menus\.

   1. Copy the **Public key** for the Route 53 registrar\. In the **Manage DNSSEC keys** dialog, paste the value into the **Public key** box\.

   1. Choose **Add**\.

1. Wait for the updates to propagate, based on the TTL for your domain records\.

**Note**  
Your new records take time to propagate to the Route 53 DNS servers\. Currently, the only way to verify that changes have propagated is to use the [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) action\. Changes generally propagate to all Route 53 name servers within 60 seconds\.

## Enabling DNSSEC signing with an existing KSK<a name="dns-configuring-dnssec-enable-existing-ksk"></a>

If you already have at least one key\-signing key \(KSK\), you can enable DNSSEC signing for a hosted zone using an existing KSK\. Follow these steps to enable DNSSEC signing in this scenario\.<a name="dns-configuring-dnssec-enable-existing-ksk-procedure"></a>

**To enable DNSSEC signing with an existing KSK**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone that you want to enable DNSSEC signing for\.

1. On the **DNSSEC signing** tab, choose **Enable DNSSEC signing**\.
**Note**  
If the option in this section is **Disable DNSSEC signing**, you have already completed the first step in enabling DNSSEC signing\. Be sure that you establish, or that there already exists, a chain of trust for the hosted zone for DNSSEC, and then you're done\. For more information, see [Establishing a chain of trust](#dns-configuring-dnssec-chain-of-trust)\.

1. Under **KSK**, choose **Use the active KSK** or **Create a new KSK**\.

1. If you choose to create a new KSK, enter the alias for a customer managed CMK that applies to DNSSEC signing, or enter an alias for a new customer managed CMK\.
**Note**  
If you choose to have Route 53 create a customer managed CMK, be aware that separate charges apply for each customer managed CMK\. For more information, see [AWS Key Management Service pricing](https://aws.amazon.com/kms/pricing/)\.

1. Choose **Enable DNSSEC signing**\.