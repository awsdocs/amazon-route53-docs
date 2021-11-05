# Forwarding rules for reverse DNS queries in Resolver<a name="resolver-automatic-forwarding-rules-reverse-dns"></a>

When the `enableDnsHostnames` and `enableDnsSupport` are set to `true` for a virtual private cloud \(VPC\) from Amazon VPC, Resolver automatically creates auto\-defined forward rules for reverse DNS queries and localhost\-related domains\. For more information about these settings, see [DNS attributes in your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-dns-support) in the *Amazon VPC Developer Guide*\.

Forwarding rules for reverse DNS queries are particularly useful for services like SSH or Active Directory, which have an option to authenticate users by performing a reverse DNS lookup for the IP address from which a customer is attempting to connect to a resource\. For more information about auto\-defined system rules, see [Domain names that Resolver creates autodefined system rules for](resolver.md#resolver-overview-forward-vpc-to-network-autodefined-rules)\. 

You can turn off these rules and modify all reverse DNS queries so that they are, for example, forwarded to your on\-premises name servers for resolution\.

After you turn off the automatic rules, create rules to forward the queries as needed to your on\-premises resources\. For more information ablout how to manage forwarding rules, see [Managing forwarding rules](resolver-rules-managing.md)\.<a name="resolver-automatic-reverse-rules-disable-procedure"></a>

**To turn off auto\-defined rules**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, under **Resolver** choose **VPCs**, and then choose a VPC ID\.

1. Under **Autodefined rules for reverse DNS resolution**, deselect the check box\. If the check box is already deselected, you can select it to turn on auto\-defined reverse DNS resolution\.

For the related APIs, see [Resolver configuration APIs](https://docs.aws.amazon.com/Route53/latest/APIReference/API-actions-by-function.html#actions-by-function-resolver-configuration)\.