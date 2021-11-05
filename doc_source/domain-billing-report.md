# Downloading a domain billing report<a name="domain-billing-report"></a>

If your AWS bill is charged to a credit card, you receive a separate invoice for each domain transaction\. These invoices don't include the domain name\. If you manage multiple domains and you want to view charges by domain for a specified time period, you can download a domain billing report\. This report includes all charges that apply to domain registration, including the following:
+ Registering a domain
+ Renewing registration for a domain
+ Transferring a domain to Amazon Route 53
+ Changing the owner of a domain \(for some TLDs, this operation is free\)

**Note**  
If you use invoiced payments, any Route 53 domain registration transactions appear in your monthly AWS invoice\. The invoice includes the domain name and operation that each charge applies to\.

When you run the report using the console, you can choose the following options:
+ **Last 12 months**: The report includes charges from one year before you ran the report until the current day\. For example, if you run the report on June 3rd, it includes charges from June 3rd the previous year until the current day\.
+ **Individual months in the last year**: The report includes charges for the specified month\.

If you run the report programmatically, you can get charges for any date range, starting with July 31, 2014\. That's the date that Route 53 started to support domain registration\. For example, see [view\-billing](https://docs.aws.amazon.com/cli/latest/reference/route53domains/view-billing.html) in the *AWS CLI Command Reference*\.

The billing report, in CSV format, includes the following values:
+ The AWS invoice ID that the charge appears on\.
+ The operation \(REGISTER\_DOMAIN, RENEW\_DOMAIN, TRANSFER\_IN\_DOMAIN, or CHANGE\_DOMAIN\_OWNER\)\.
+ The name of the domain\.
+ The charge for the operation in US dollars\.
+ The date and time in ISO 8601 format, for example, 2016\-03\-03T19:20:25\.177Z\. For more information about ISO 8601 format, see the Wikipedia article [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)\.<a name="domain-billing-report-procedure"></a>

**To download a domain billing report**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose **Domain billing report**\.

1. Choose the date range for the report, and then choose **Download domain report**\.

1. Follow the prompts to open the report or to save it\.

1. If you encounter issues while downloading a domain billing report, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.