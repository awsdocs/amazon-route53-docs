# Extending the registration period for a domain<a name="domain-extend"></a>

When you register a domain with Amazon Route 53 or you transfer domain registration to Route 53, we configure the domain to renew automatically\. The automatic renewal period is typically one year, although the registries for some top\-level domains \(TLDs\) have longer renewal periods\. 

Note the following:

**Maximum renewal period**  
All generic TLDs and many country\-code TLDs let you extend domain registration for longer periods, typically up to ten years in one\-year increments\. To determine whether you can extend the registration period for your domain, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\. If longer registration periods are allowed, perform the following procedure\.

**Restrictions on when you can renew or extend a domain registration**  
Some TLD registries have restrictions on when you can renew or extend a domain registration, for example, the last two months before the domain expires\. Even if the registry allows extending the registration period for a domain, they might not allow it at the current number of days before the domain expires\.

**AWS credits**  
You can't use AWS credits to pay the fee for extending the registration period for a domain\.<a name="domain-extend-procedure"></a>

**To extend the registration period for your domain**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain for which you want to extend the registration period\.

   The **Expires on** field lists the current expiration date for the domain\. If the registry for the TLD allows extending the registration period, an **extend** link appears on the right side of the expiration date\.

1. Choose **extend**\.

1. In the **Extend registration for** list, choose the number of years that you want to extend the registration for\.

   The list shows all the current options based on the current expiration date and the maximum registration period allowed by the registry for this domain\. The **New expiration date** field shows the expiration date with that number of years applied\.

1. Choose **Extend domain registration**\.

   When we receive confirmation from the registry that they've updated your expiration date, we send you an email to confirm that we've changed the expiration date\.

1. **AISPL \(India\) customers only**: If your contact address is in India, your user agreement is with Amazon Internet Services Pvt\. Ltd \(AISPL\), a local AWS seller in India\. To extend the registration for a domain, perform the following steps to pay the fee for the extension\. 

   1. Go to the [Orders and Invoices](https://console.aws.amazon.com/billing/home#/paymenthistory) page in the AWS Management Console\.

   1. In the **Payments Due** section, find the applicable invoice\.

   1. In the **Actions** column, choose **Verify and Pay**\.

      After you pay the invoice, we complete the extension and send the applicable emails\.
**Important**  
If you don't pay the invoice within five days, the invoice is canceled\. To extend the domain registration after an invoice is canceled, resubmit the request\.

   For more information, see [Managing your payments in India](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/edit-aispl-payment-method.html) in the *AWS Billing and Cost Management User Guide*\.

1. If you encounter issues while extending the registration period for a domain, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.