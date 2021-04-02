# Enabling DNSSEC validation in Amazon Route 53<a name="resolver-dnssec-validation"></a>

When you enable DNSSEC validation for a virtual private cloud \(VPC\) in Amazon Route 53, DNSSEC signatures are cryptographically checked to ensure that the response was not tampered with\. You enable DNSSEC validation on your VPC detail page\. 

DNSSEC validation only applies to public signed names in Amazon Route 53, and not to forwarded zones\.

**Important**  
Enabling DNSSEC validation can impact DNS resolution for public DNS records from AWS resources in a VPC, which could result in an outage\. Be aware that enabling or disabling DNSSEC validation can take several minutes\. <a name="resolver-dnssec-validation-procedure"></a>

**To enable DNSSEC validation for a VPC**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, under **Resolver**, choose **VPCs**\.

1. Under the **VPC name** column, choose a VPC\.

1. Under **DNSSEC validation**, select the checkbox\. If the checkbox is already selected, you can clear it to disable DNSSEC validation\.

   Be aware that enabling or disabling DNSSEC validation can take several minutes\.