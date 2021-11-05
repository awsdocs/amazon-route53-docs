# My domain is suspended \(status is ClientHold\)<a name="troubleshooting-domain-suspended"></a>

If Amazon Route 53 suspends your domain, the domain becomes unavailable on the internet\. You can use either of the following methods to determine whether a domain has been suspended:
+ On the **Registered domains** page of the Route 53 console, find the domain name in the **Alerts** table at the bottom of the page\. If the value of the **Status** column is **clientHold**, the domain has been suspended\.
+ Send a WHOIS query for the domain\. If the value of **Domain Status** is **clientHold**, the domain has been suspended\. The WHOIS command is available in many operating systems, and it's also available as a web application on many websites\.

In addition, when we suspend a domain, we generally send an email to the email address for the registrant contact for the domain\. However, if the domain was suspended based on a court order, the court might not let us notify the registrant contact\.

To make a domain available on the internet again, you must get it unsuspended\. Here are the reasons that a domain can be suspended and how you get it unsuspended\.

**Note**  
If you need help getting your domain unsuspended, you can contact AWS Support free of charge\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

**Topics**
+ [You registered a new domain, but you didn't click the link in the confirmation email](#troubleshooting-domain-suspended-click-link)
+ [You disabled automatic renewal for the domain, and the domain expired](#troubleshooting-domain-suspended-automatic-renewal-disabled)
+ [You changed the email address for the registrant contact, but you didn't verify that the new email address is valid](#troubleshooting-domain-suspended-new-email-not-verified)
+ [We couldn't process your payment for automatic domain renewal, and the domain expired](#troubleshooting-domain-suspended-process-payment)
+ [We suspended the domain for a violation of the AWS Acceptable Use Policy](#troubleshooting-domain-suspended-acceptable-use)
+ [We suspended the domain because of a court order](#troubleshooting-domain-suspended-court-order)

## You registered a new domain, but you didn't click the link in the confirmation email<a name="troubleshooting-domain-suspended-click-link"></a>

When you register a domain with AWS for the first time, ICANN requires that we get confirmation that the email address for the registrant contact is valid\. To get confirmation, we send an email that contains a link\. You have between 3 and 15 days to click the link, depending on the top\-level domain\. After that time, the link stops working\.

**Note**  
If you don't respond to the first email, we resend the email up to two more times\. If you have already registered one or more domains with Amazon Route 53 and used the same email address for the registrant contact, we don't send a confirmation email\. 

If you don't click the link in the email in the allotted amount of time, ICANN requires that we suspend the domain\. For information about how to resend the confirmation email to the registrant contact, see [Resending authorization and confirmation emails](domain-click-email-link.md)\. When you confirm that the email address is valid, we automatically unsuspend the domain\.

## You disabled automatic renewal for the domain, and the domain expired<a name="troubleshooting-domain-suspended-automatic-renewal-disabled"></a>

When automatic renewal is enabled for a domain \(the default value for a new or transferred domain\), we automatically renew registration for the domain shortly before the expiration date\. If you disable automatic renewal, we send three reminder emails that the domain registration is about to expire to the email address for the registrant contact\. We start to send these emails 45 days before the domain expires\.

If you disable automatic renewal for the domain and you don't manually extend the registration period for the domain, we generally suspend the domain on the expiration date\. Note that the registries for some domains delete the domain even before the expiration date\.

For information about how to renew an expired domain, see [Renewing registration for a domain](domain-renew.md)\.

## You changed the email address for the registrant contact, but you didn't verify that the new email address is valid<a name="troubleshooting-domain-suspended-new-email-not-verified"></a>

If you change the email address for the registrant contact to an address that you haven't previously verified, ICANN requires that we get confirmation that the email address for the registrant contact is valid\. To get confirmation, we send an email that contains a link\. You have between 3 and 15 days to click the link, depending on the top\-level domain\. After that time, the link stops working\.

If you don't click the link in the email in the amount of time allowed by the TLD registry, ICANN requires that we suspend the domain\. For information about how to resend the confirmation email to the registrant contact, see [Resending authorization and confirmation emails](domain-click-email-link.md)\. When you confirm that the email address is valid, we automatically unsuspend the domain\.

## We couldn't process your payment for automatic domain renewal, and the domain expired<a name="troubleshooting-domain-suspended-process-payment"></a>

If automatic renewal is enabled for a domain but we weren't able to process your payment \(for example, because your credit card expired\), we send several emails to the email address for the registrant contact for the domain\. If we don't receive payment, we generally suspend the domain on the expiration date\. Note that the registries for some domains delete the domain even before the expiration date\.

For information about how to renew an expired domain, see [Renewing registration for a domain](domain-renew.md)\.

## We suspended the domain for a violation of the AWS Acceptable Use Policy<a name="troubleshooting-domain-suspended-acceptable-use"></a>

If we suspend a domain for a violation of the [AWS Acceptable Use Policy](https://aws.amazon.com/aup/), we send an email notification to the registrant contact for the domain\. \(We don't send a notification email if the AWS account is already suspended for fraud\.\) 

To contest a suspension, send an email to abuse@amazon\.com\.

## We suspended the domain because of a court order<a name="troubleshooting-domain-suspended-court-order"></a>

If a domain is suspended as a result of a court order, we can't unsuspend the domain until the court order has been lifted\. To contest the validity of a court order, send an email to abuse@amazon\.com and attach the applicable documents\.