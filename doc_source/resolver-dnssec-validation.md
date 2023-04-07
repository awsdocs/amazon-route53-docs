# Enabling DNSSEC validation in Amazon Route 53<a name="resolver-dnssec-validation"></a>

When you enable DNSSEC validation for a virtual private cloud \(VPC\) in Amazon Route 53, DNSSEC signatures are cryptographically checked to ensure that the response was not tampered with\. You enable DNSSEC validation on your VPC detail page\. 

DNSSEC validation only applies to public signed names in Amazon Route 53, and not to forwarded zones\.

**Important**  
Enabling DNSSEC validation can impact DNS resolution for public DNS records from AWS resources in a VPC, which could result in an outage\. Be aware that enabling or disabling DNSSEC validation can take several minutes\. 

**Note**  
At this time, the Amazon Route 53 Resolver in your VPC \(aka AmazonProvidedDNS\) ignores the DO \(DNSSEC OK\) EDNS header bit and the CD \(Checking Disabled\) bit in the DNS query\. If you have configured DNSSEC, this means that while the Route 53 Resolver does perform DNSSEC validation, it doesn't return DNSSEC records nor set the AD bit in the response\. Therefore, performing your own DNSSEC validation is not currently supported by the Route 53 Resolver\. If you need to do this you will have to perform your own recursive DNS resolution\.<a name="resolver-dnssec-validation-procedure"></a>

**To enable DNSSEC validation for a VPC**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, under **Resolver**, choose **VPCs**\.

1. Under **DNSSEC validation**, select the check box\. If the check box is already selected, you can clear it to disable DNSSEC validation\.

   Be aware that enabling or disabling DNSSEC validation can take several minutes\.