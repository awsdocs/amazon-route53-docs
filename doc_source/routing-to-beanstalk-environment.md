# Routing traffic to an AWS Elastic Beanstalk environment<a name="routing-to-beanstalk-environment"></a>

If you're using AWS Elastic Beanstalk to deploy and manage applications in the AWS Cloud, you can use Amazon Route 53 to route DNS traffic for your domain, such as example\.com, to a new or an existing Elastic Beanstalk environment\.

To route DNS traffic to an Elastic Beanstalk environment, see the procedures in the following topics\.

**Note**  
These procedures assume that you're already using Route 53 as the DNS service for your domain\. If you're using another DNS service, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md) for information about using Route 53 as the DNS service provider for your domain\. 

**Topics**
+ [Deploying an application into an Elastic Beanstalk environment](#routing-to-beanstalk-environment-deploy)
+ [Getting the domain name for your Elastic Beanstalk environment](#routing-to-beanstalk-environment-get-domain-name)
+ [Creating an Amazon Route 53 record that routes traffic to your Elastic Beanstalk environment](#routing-to-beanstalk-environment-create-resource-record-set)

## Deploying an application into an Elastic Beanstalk environment<a name="routing-to-beanstalk-environment-deploy"></a>

If you already have an Elastic Beanstalk environment that you want to route traffic to, skip to [Getting the domain name for your Elastic Beanstalk environment](#routing-to-beanstalk-environment-get-domain-name)\.

**To create an application and deploy it into an Elastic Beanstalk environment**
+ For information about creating an application and deploying it to an Elastic Beanstalk environment, see [Getting started using Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/GettingStarted.html) in the *AWS Elastic Beanstalk Developer Guide*\.

## Getting the domain name for your Elastic Beanstalk environment<a name="routing-to-beanstalk-environment-get-domain-name"></a>

If you already know the domain name for your Elastic Beanstalk environment, skip to [Creating an Amazon Route 53 record that routes traffic to your Elastic Beanstalk environment](#routing-to-beanstalk-environment-create-resource-record-set)\.<a name="routing-to-beanstalk-environment-get-domain-name-procedure"></a>

**To get the domain name for your Elastic Beanstalk environment**

1. Sign in to the AWS Management Console and open the Elastic Beanstalk console at [https://console\.aws\.amazon\.com/elasticbeanstalk/](https://console.aws.amazon.com/elasticbeanstalk/)\.

1. In the list of applications, find the application that you want to route traffic to, and get the value of **URL**\.

## Creating an Amazon Route 53 record that routes traffic to your Elastic Beanstalk environment<a name="routing-to-beanstalk-environment-create-resource-record-set"></a>

An Amazon Route 53 record contains the settings that control how traffic is routed to your Elastic Beanstalk environment\. You create either a *CNAME record* or an *alias record*, depending on whether the domain name for the environment includes the Region, such as **us\-east\-2**, in which you deployed the environment\. New environments include the Region in the domain name; environments that were created before early 2016 do not\. For a comparison of CNAME and alias records, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**If the domain name does not include the Region**  
You must create a *CNAME record*\. However, because of limitations imposed by DNS, you can create CNAME records only for subdomains, not for the root domain name\. For example, if your domain name is example\.com, you can create a record that routes traffic for acme\.example\.com to your Elastic Beanstalk environment, but you can't create a record that routes traffic for example\.com to your Elastic Beanstalk environment\.  
See the procedure [To create a CNAME record to route traffic to an Elastic Beanstalk environment](#routing-to-beanstalk-environment-create-cname-procedure)\.

**If the domain name includes the Region**  
You can create an alias record\. An alias record is specific to Route 53 and has two significant advantages over CNAME records:  
+ You can create alias records for the root domain name or for subdomains\. For example, if your domain name is example\.com, you can create a record that routes requests for example\.com or for acme\.example\.com to your Elastic Beanstalk environment\.
+ Route 53 doesn't charge for requests that use an alias record to route traffic\.
See the procedure [To create an Amazon Route 53 alias record to route traffic to an Elastic Beanstalk environment](#routing-to-beanstalk-environment-create-alias-procedure)\.<a name="routing-to-beanstalk-environment-create-cname-procedure"></a>

**To create a CNAME record to route traffic to an Elastic Beanstalk environment**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that you want to use to route traffic to your Elastic Beanstalk environment\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Enter the domain name that you want to use to route traffic to your Elastic Beanstalk environment\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use acme\.example\.com to route traffic to your environment, enter **acme**\.  
You can't create a CNAME record that has the same name as the hosted zone\.  
**Type**  
Choose **CNAME – Canonical name**\.  
**Alias**  
Choose **No**\.  
**TTL \(Seconds\)**  
Accept the default value of **300**\.  
**Value**  
Enter the domain name of the environment that you want to route traffic to\. This is the value that you get when you perform the procedure in the topic [Getting the domain name for your Elastic Beanstalk environment](#routing-to-beanstalk-environment-get-domain-name)\.  
**Routing Policy**  
Choose the applicable routing policy\. For more information, see [Choosing a routing policy](routing-policy.md)\.

1. Choose **Create**\.

   Changes generally propagate to all Route 53 servers within 60 seconds\. <a name="routing-to-beanstalk-environment-create-alias-procedure"></a>

**To create an Amazon Route 53 alias record to route traffic to an Elastic Beanstalk environment**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that you want to use to route traffic to your Elastic Beanstalk environment\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Enter the domain name that you want to use to route traffic to your Elastic Beanstalk environment\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use acme\.example\.com to route traffic to your environment, enter **acme**\.  
**Type**  
Accept the default, **A – Ipv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
Click in the field, and choose the domain name of the environment that you want to route traffic to\. This is the value that you get when you perform the procedure in the topic [Getting the domain name for your Elastic Beanstalk environment](#routing-to-beanstalk-environment-get-domain-name)\.  
If you used different accounts to create your Route 53 hosted zone and your Elastic Beanstalk environment, enter the CNAME attribute for the Elastic Beanstalk environment\.   
**Alias Hosted Zone ID**  
This value appears automatically based on the environment that you choose for **Alias Target**\.  
**Routing Policy**  
Choose the applicable routing policy\. For more information, see [Choosing a routing policy](routing-policy.md)\.  
**Evaluate Target Health**  
Accept the default value, **No**\.

1. Choose **Create**\.

   Changes generally propagate to all Route 53 servers within 60 seconds\. When propagation is done, you'll be able to route traffic to your Elastic Beanstalk environment by using the name of the alias record that you create in this procedure\. 