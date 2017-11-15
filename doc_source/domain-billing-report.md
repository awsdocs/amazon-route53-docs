# Downloading a Domain Billing Report<a name="domain-billing-report"></a>

AWS invoices don't include the domain name for domain registration charges\. If you manage multiple domains and you want to view charges by domain for a specified time period, you can download a domain billing report\. This report includes all charges that apply to domain registration, including the following:

+ Registering a domain

+ Renewing registration for a domain

+ Transferring a domain to Amazon Route 53

+ Changing the owner of a domain \(for some TLDs, this operation is free\)

The billing report, in CSV format, includes the following values:

+ The AWS invoice ID that the charge appears on\.

+ The operation \(REGISTER\_DOMAIN, RENEW\_DOMAIN, TRANSFER\_IN\_DOMAIN, or CHANGE\_DOMAIN\_OWNER\)\.

+ The name of the domain\.

+ The charge for the operation in US dollars\.

+ The date and time in ISO 8601 format, for example, 2016\-03\-03T19:20:25\.177Z\. For more information about ISO 8601 format, see the Wikipedia article [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)\.

**To download a domain billing report**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose **Domain billing report**\.

1. Choose the date range for the report, and then choose **Download domain report**\.

1. Follow the prompts to open the report or to save it\.