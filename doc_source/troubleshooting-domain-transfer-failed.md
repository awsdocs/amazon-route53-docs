# Transferring my domain to Amazon Route 53 failed<a name="troubleshooting-domain-transfer-failed"></a>

Here are some common reasons that transferring a domain to Amazon Route 53 fails\.

**Topics**
+ [You didn't click the link in the authorization email](#troubleshooting-domain-transfer-failed-click-link)
+ [The authorization code that you got from the current registrar is not valid](#troubleshooting-domain-transfer-failed-authorization-code-invalid)
+ ["Parameters in request are not valid" error when trying to transfer a \.es domain to Amazon Route 53](#troubleshooting-domain-transfer-failed-parameters-in-request-are-not-valid)

## You didn't click the link in the authorization email<a name="troubleshooting-domain-transfer-failed-click-link"></a>

When you transfer domain registration to Amazon Route 53, we're required by ICANN, the governing body for domain registration, to get authorization for the transfer from the registrant contact for the domain\. To get authorization, we send you an email that contains a link\. You have between 5 and 15 days to click the link, depending on the top\-level domain\. After that time, the link stops working\.

If you don't click the link in the email in the allotted amount of time, ICANN requires that we cancel the transfer\. For information about how to resend the authorization email to the registrant contact, see [Resending authorization and confirmation emails](domain-click-email-link.md)\.

## The authorization code that you got from the current registrar is not valid<a name="troubleshooting-domain-transfer-failed-authorization-code-invalid"></a>

If you request the transfer of a domain to Amazon Route 53 and you don't receive the authorization email, check [the status page in the Route 53 console](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-transfer-to-route-53-status.html)\. If the status page shows that the transfer authorization code that you got from your registrar is not valid, perform the following steps:

1. Contact the current registrar for the domain and request a new authorization code\. Confirm the following:
   + How long the new authorization code will remain active\. You must request a domain transfer before the code expires\.
   + The new authorization code is different from the code that isn't valid\. If not, ask the current registrar to refresh the authorization code\.

1. Submit another request to transfer the domain\. For more information, see [Step 5: Request the transfer](domain-transfer-to-route-53.md#domain-transfer-to-route-53-request-transfer) in the topic [Transferring registration for a domain to Amazon Route 53](domain-transfer-to-route-53.md)\.

## "Parameters in request are not valid" error when trying to transfer a \.es domain to Amazon Route 53<a name="troubleshooting-domain-transfer-failed-parameters-in-request-are-not-valid"></a>

Amazon Route 53 returns a "Parameters in request are not valid" error when you try to transfer a \.es domain to Route 53 and the contact type of the registrant contact is **Company**\. To complete the transfer, open a case with AWS Support:

1. Sign in to the [AWS Support Center](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=customer-service&serviceCode=billing&categoryCode=domain-name-registration-issue)\.

1. Specify the following values:  
**Regarding**  
Accept the default value of **Account and Billing Support**\.  
**Service**  
Accept the default value of **Billing**\.  
**Category**  
Accept the default value of **Domain name registration issue**\.  
**Subject**  
Specify **Parameters in request are not valid error**\.  
**Description**  
Specify the name of the domain that you want to transfer\.  
**Contact method**  
Specify a contact method and enter the applicable values\.

1. Choose **Submit**\.