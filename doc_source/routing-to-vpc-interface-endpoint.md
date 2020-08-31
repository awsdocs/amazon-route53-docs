# Routing traffic to an Amazon Virtual Private Cloud interface endpoint by using your domain name<a name="routing-to-vpc-interface-endpoint"></a>

An Amazon Virtual Private Cloud \(Amazon VPC\) interface endpoint lets you use AWS PrivateLink to access selected services\. These services include some AWS services, services that are hosted by other AWS customers and partners in their own VPCs, and supported AWS Marketplace partner services\.

To route domain traffic to an interface endpoint, use Amazon Route 53 to create an alias record\. An alias record is a Route 53 extension to DNS\. It's similar to a CNAME record, but you can create an alias record both for the root domain, such as example\.com, and for subdomains, such as www\.example\.com\. \(You can create CNAME records only for subdomains\.\)

**Note**  
Route 53 doesn't charge for alias queries to interface endpoints or other AWS resources\.

**Topics**
+ [Prerequisites](#routing-to-vpc-interface-endpoint-prereqs)
+ [Configuring Amazon Route 53 to route traffic to an Amazon VPC interface endpoint](#routing-to-vpc-interface-endpoint-config)

## Prerequisites<a name="routing-to-vpc-interface-endpoint-prereqs"></a>

Before you get started, you need the following:
+ An Amazon VPC interface endpoint\. For more information, see [Interface VPC endpoints \(AWS PrivateLink\)](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) in the *Amazon VPC User Guide*\.
+ A registered domain name\. You can use Amazon Route 53 as your domain registrar, or you can use a different registrar\.
+ Route 53 as the DNS service for the domain\. If you register your domain name by using Route 53, we automatically configure Route 53 as the DNS service for the domain\. 

  For information about using Route 53 as the DNS service provider for your domain, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

## Configuring Amazon Route 53 to route traffic to an Amazon VPC interface endpoint<a name="routing-to-vpc-interface-endpoint-config"></a>

To configure Amazon Route 53 to route traffic to an Amazon VPC interface endpoint, perform the following procedure\.<a name="routing-to-vpc-interface-endpoint-config-procedure"></a>

**To route traffic to an Amazon VPC interface endpoint**

1. If you created the Route 53 hosted zone and the Amazon VPC interface endpoint using the same account, skip to step 2\.

   If you created the hosted zone and the interface endpoint using different accounts, get the service name for the interface endpoint:

   1. Sign in to the AWS Management Console and open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

   1. In the navigation pane, choose **Endpoints**\.

   1. In the right pane, choose the endpoint that you want to route internet traffic to\.

   1. In the bottom pane, get the value of DNS name, for example, **vpce\-0fd00dd593example\-dexample\.cloudtrail\.us\-west\-2\.vpce\.amazonaws\.com**\.

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that has the domain name that you want to use to route traffic to your interface endpoint\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Enter the domain name that you want to use to route traffic to your Amazon VPC interface endpoint\.   
**Type**  
Choose **A – IPv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
How you specify the value for **Alias Target** depends on whether you created the hosted zone and the interface endpoint using the same AWS account or different accounts:  
   + **Same account** – Choose the list, and find the category **Amazon VPC Endpoints**\. Then choose the DNS name of the interface endpoint that you want to route internet traffic to\.
   + **Different accounts** – Enter the value that you got in step 1 of this procedure\.  
**Routing Policy**  
Choose the applicable routing policy\. For more information, see [Choosing a routing policy](routing-policy.md)\.  
**Evaluate Target Health**  
Choose **No**\.

1. Choose **Create**\.

   Changes generally propagate to all Route 53 servers within 60 seconds\. When propagation is done, you'll be able to route traffic to your interface endpoint by using the name of the alias record that you created in this procedure\.