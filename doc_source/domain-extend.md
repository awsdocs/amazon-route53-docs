# Extending the Registration Period for a Domain<a name="domain-extend"></a>

When you register a domain with Amazon Route 53 or you transfer domain registration to Route 53, we configure the domain to renew automatically\. The automatic renewal period is typically one year, although the registries for some top\-level domains \(TLDs\) have longer renewal periods\. 

All generic TLDs and many country\-code TLDs let you extend domain registration for longer periods, typically up to ten years in one\-year increments\. To determine whether you can extend the registration period for your domain, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\. If longer registration periods are allowed, perform the following procedure\.

**Note**  
Some TLD registries have restrictions on when you can renew or extend a domain registration, for example, the last two months before the domain expires\. Even if the registry allows extending the registration period for a domain, they might not allow it at the current number of days before the domain expires\.

Note that you can't use AWS credits to pay the fee for extending the registration period for a domain\.

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