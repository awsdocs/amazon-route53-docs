# Routing traffic to an Amazon API Gateway API by using your domain name<a name="routing-to-api-gateway"></a>

Amazon API Gateway lets you create, publish, maintain, monitor, and secure APIs\. You can create APIs that access AWS services or other web services, as well as data stored in the AWS Cloud\.

The method that you use to route domain traffic to an API Gateway API depends on whether you created a regional API Gateway endpoint or an edge\-optimized API Gateway endpoint\. 
+ **Regional API endpoint**: You create a Route 53 alias record that routes traffic to the regional API endpoint\.
+ **Edge\-optimized API endpoint**: You create a Route 53 alias record that routes traffic to the edge\-optimized API\. This causes traffic to be routed to the CloudFront distribution that's associated with the edge\-optimized API\.

An alias record is a Route 53 extension to DNS that's similar to a CNAME record\. For a comparison of alias and CNAME records, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**Note**  
Route 53 doesn't charge for alias queries to API Gateway APIs or other AWS resources\.

**Topics**
+ [Prerequisites](#routing-to-api-gateway-prereqs)
+ [Configuring Route 53 to route traffic to a regional API Gateway endpoint](#routing-to-api-gateway-config)
+ [Configuring Route 53 to route traffic to an edge\-optimized API Gateway endpoint](#routing-to-api-gateway-config-edge-optimized)

## Prerequisites<a name="routing-to-api-gateway-prereqs"></a>

Before you get started, you need the following:
+ An API Gateway API that has a custom domain name, such as api\.example\.com, that matches the name of the Route 53 record that you want to create\.
+ A registered domain name\. You can use Amazon Route 53 as your domain registrar, or you can use a different registrar\.
+ Route 53 as the DNS service for the domain\. If you register your domain name by using Route 53, we automatically configure Route 53 as the DNS service for the domain\. 

  For information about using Route 53 as the DNS service provider for your domain, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

## Configuring Route 53 to route traffic to a regional API Gateway endpoint<a name="routing-to-api-gateway-config"></a>

To configure Route 53 to route traffic to a regional API Gateway endpoint, perform the following procedure\.<a name="routing-to-api-gateway-config-procedure"></a>

**To route traffic to a regional API Gateway endpoint**

1. If you created the Route 53 hosted zone and the regional endpoint using the same account, skip to step 2\.

   If you created the hosted zone and the regional endpoint using different accounts, get the target domain name for the custom domain name that you want to use:

   1. Sign in to the AWS Management Console and open the API Gateway console at [https://console\.aws\.amazon\.com/apigateway/](https://console.aws.amazon.com/apigateway/)\. 

   1. In the navigation pane, choose **Custom domain names**\.

   1. For the custom domain name that you want to use, get the value of ** API Gateway domain name**, for example, **d\-gy061cuws5\.execute\-api\.*region*\.amazonaws\.com**\.

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that has the domain name that you want to use to route traffic to your API\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Enter the domain name that you want to use to route traffic to your API\.   
The API that you want to route traffic to must include a custom domain name, such as api\.example\.com, that matches the name of the Route 53 record\.  
**Type**  
Choose **A – IPv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
How you specify the value for **Alias Target** depends on whether you created the hosted zone and the API using the same AWS account or different accounts:  
   + **Same account** – Choose the list, and find the category **API Gateway APIs**\. The list of target domain names includes only APIs that have a custom domain name that matches the value that you specified for **Name**\. Choose the applicable value\.
   + **Different accounts** – Enter the value that you got in step 1 of this procedure\.  
**Routing Policy**  
Choose the applicable routing policy\. For more information, see [Choosing a routing policy](routing-policy.md)\.  
**Evaluate Target Health**  
Accept the default value of **No**\.

1. Choose **Create**\.

   Changes generally propagate to all Route 53 servers within 60 seconds\. When propagation is done, you'll be able to route traffic to your API by using the name of the alias record that you created in this procedure\.

## Configuring Route 53 to route traffic to an edge\-optimized API Gateway endpoint<a name="routing-to-api-gateway-config-edge-optimized"></a>

To configure Route 53 to route traffic to an edge\-optimized API Gateway endpoint, perform the following procedure\. <a name="routing-to-api-gateway-config-edge-optimized-procedure"></a>

**To route traffic to an edge\-optimized API Gateway endpoint**

1. If you created the Route 53 hosted zone and the regional endpoint using the same account, skip to step 2\. 

   If you created the hosted zone and the regional endpoint using different accounts, get the target domain name for the custom domain name that you want to use: 

   1. Sign in to the AWS Management Console and open the API Gateway console at [https://console\.aws\.amazon\.com/apigateway/](https://console.aws.amazon.com/apigateway/)\. 

   1. In the navigation pane, choose **Custom domain names**\.

   1. For the custom domain name that you want to use, get the value of **Domain name**\.

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that has the domain name that you want to use to route traffic to your API\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Enter the domain name that you want to use to route traffic to your API\.   
The API that you want to route traffic to must include a custom domain name, such as api\.example\.com, that matches the name of the Route 53 record\.  
**Type**  
Choose **A – IPv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
How you specify the value for **Alias Target** depends on whether you created the hosted zone and the API using the same AWS account or different accounts:  
   + **Same account** – Choose the list, and find the category **CloudFront distributions**\. The list of target domain names includes only distributions that have a custom domain name that matches the value that you specified for **Name**\. Choose the applicable value\.
   + **Different accounts** – Enter the value that you got in steps 1a through 1c of this procedure\.  
**Routing Policy**  
Choose the applicable routing policy\. For more information, see [Choosing a routing policy](routing-policy.md)\.  
**Evaluate Target Health**  
Accept the default value of **No**\.

1. Choose **Create**\.

   Changes generally propagate to all Route 53 servers within 60 seconds\. When propagation is done, you can route traffic to your API by using the name of the alias record that you created in this procedure\.