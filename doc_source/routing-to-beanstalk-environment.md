# Routing Traffic to an AWS Elastic Beanstalk Environment<a name="routing-to-beanstalk-environment"></a>

If you're using AWS Elastic Beanstalk to deploy and manage applications in the AWS Cloud, you can use Amazon Route 53 to route DNS traffic for your domain, such as example\.com, to a new or an existing Elastic Beanstalk environment\.

To route DNS traffic to an Elastic Beanstalk environment, see the procedures in the following topics\.

**Note**  
These procedures assume that you're already using Amazon Route 53 as the DNS service for your domain\. If you're using another DNS service, see [Using Amazon Route 53 as the DNS Service for Subdomains Without Migrating the Parent Domain](creating-migrating.md) for information about migrating your DNS service to Amazon Route 53\. 


+ [Deploying an Application into an Elastic Beanstalk Environment](#routing-to-beanstalk-environment-deploy)
+ [Getting the Domain Name for Your Elastic Beanstalk Environment](#routing-to-beanstalk-environment-get-domain-name)
+ [Creating an Amazon Route 53 Resource Record Set that Routes Traffic to Your Elastic Beanstalk Environment](#routing-to-beanstalk-environment-create-resource-record-set)

## Deploying an Application into an Elastic Beanstalk Environment<a name="routing-to-beanstalk-environment-deploy"></a>

If you already have an Elastic Beanstalk environment that you want to route traffic to, skip to [Getting the Domain Name for Your Elastic Beanstalk Environment](#routing-to-beanstalk-environment-get-domain-name)\.

**To create an application and deploy it into an Elastic Beanstalk environment**

+ For information about creating an application and deploying it to an Elastic Beanstalk environment, see [Getting Started Using Elastic Beanstalk](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/GettingStarted.html) in the *AWS Elastic Beanstalk Developer Guide*\.

## Getting the Domain Name for Your Elastic Beanstalk Environment<a name="routing-to-beanstalk-environment-get-domain-name"></a>

If you already know the domain name for your Elastic Beanstalk environment, skip to [Creating an Amazon Route 53 Resource Record Set that Routes Traffic to Your Elastic Beanstalk Environment](#routing-to-beanstalk-environment-create-resource-record-set)\.

**To get the domain name for your Elastic Beanstalk environment**

1. Sign in to the AWS Management Console and open the Elastic Beanstalk console at [https://console\.aws\.amazon\.com/elasticbeanstalk/](https://console.aws.amazon.com/elasticbeanstalk/)\.

1. In the list of applications, find the application that you want to route traffic to, and get the value of **URL**\.

## Creating an Amazon Route 53 Resource Record Set that Routes Traffic to Your Elastic Beanstalk Environment<a name="routing-to-beanstalk-environment-create-resource-record-set"></a>

An Amazon Route 53 resource record set contains the settings that control how traffic is routed to your Elastic Beanstalk environment\. You create either a *CNAME resource record set* or an *alias resource record set*, depending on whether the domain name for the environment includes the region, such as **us\-east\-2**, in which you deployed the environment\. New environments include the region in the domain name; environments that were created before early 2016 do not\. For a comparison of CNAME and alias resource record sets, see [Choosing Between Alias and Non\-Alias Resource Record Sets](resource-record-sets-choosing-alias-non-alias.md)\.

**If the domain name does not include the region**  
You must create a *CNAME resource record set*\. You can't create a CNAME resource record set for the root domain name\. For example, if your domain name is example\.com, you can create a resource record set that routes traffic for acme\.example\.com to your Elastic Beanstalk environment, but you can't create a resource record set that routes traffic for example\.com to your Elastic Beanstalk environment\.  
See the procedure [To create a CNAME resource record set to route traffic to an Elastic Beanstalk environment](#routing-to-beanstalk-environment-create-cname-procedure)\.

**If the domain name includes the region**  
You can create an alias resource record set\. An alias resource record set is specific to Amazon Route 53 and has two significant advantages over CNAME resource record sets:  

+ You can create alias resource record sets for the root domain name or for subdomains\. For example, if your domain name is example\.com, you can create a resource record set that routes requests for example\.com or for acme\.example\.com to your Elastic Beanstalk environment\.

+ Amazon Route 53 doesn't charge for requests that use an alias resource record set to route traffic\.
See the procedure [To create an Amazon Route 53 alias resource record set to route traffic to an Elastic Beanstalk environment](#routing-to-beanstalk-environment-create-alias-procedure)\.

**To create a CNAME resource record set to route traffic to an Elastic Beanstalk environment**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that you want to use to route traffic to your Elastic Beanstalk environment\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Type the domain name that you want to use to route traffic to your Elastic Beanstalk environment\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use acme\.example\.com to route traffic to your environment, type **acme**\.  
You can't create a CNAME record that has the same name as the hosted zone\.  
**Type**  
Choose **CNAME – Canonical name**\.  
**Alias**  
Choose **No**\.  
**TTL \(Seconds\)**  
Accept the default value of **300**\.  
**Value**  
Type the domain name of the environment that you want to route traffic to\. This is the value that you get when you perform the procedure in the topic [Getting the Domain Name for Your Elastic Beanstalk Environment](#routing-to-beanstalk-environment-get-domain-name)\.  
**Routing Policy**  
Accept the default value, **Simple**\.

1. Choose **Create**\.

   Changes generally propagate to all Amazon Route 53 servers within 60 seconds\. 

**To create an Amazon Route 53 alias resource record set to route traffic to an Elastic Beanstalk environment**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that you want to use to route traffic to your Elastic Beanstalk environment\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Type the domain name that you want to use to route traffic to your Elastic Beanstalk environment\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use acme\.example\.com to route traffic to your environment, type **acme**\.  
**Type**  
Accept the default, **A – Ipv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
Click in the field, and choose the domain name of the environment that you want to route traffic to\. This is the value that you get when you perform the procedure in the topic [Getting the Domain Name for Your Elastic Beanstalk Environment](#routing-to-beanstalk-environment-get-domain-name)\.  
**Alias Hosted Zone ID**  
This value appears automatically based on the environment that you choose for **Alias Target**\.  
**Routing Policy**  
Accept the default value, **Simple**\.  
**Evaluate Target Health**  
Accept the default value, **No**\.

1. Choose **Create**\.

   Changes generally propagate to all Amazon Route 53 servers within 60 seconds\. When propagation is done, you'll be able to route traffic to your Elastic Beanstalk environment by using the name of the alias resource record set that you create in this procedure\. 