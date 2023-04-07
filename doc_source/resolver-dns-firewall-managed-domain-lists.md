# Managed Domain Lists<a name="resolver-dns-firewall-managed-domain-lists"></a>

Managed Domain Lists contain domain names that are associated with malicious activity or other potential threats\. AWS maintains these lists to enable Route 53 Resolver customers to check outbound DNS queries against them for free when using DNS Firewall\. 

Keeping up to date on the constantly changing threat landscape can be time consuming and expensive\. Managed Domain Lists can save you time when you implement and use DNS Firewall\. AWS automatically updates the lists when new vulnerabilities and threats emerge\. AWS is often notified of new vulnerabilities before public disclosure, so DNS Firewall can deploy mitigations for you even, often before a new threat is become widely known\. 

Managed domain lists are designed to help protect you from common web threats and they add another layer of security for your applications\. The AWS Managed Domain Lists source their data from both internal AWS sources as well as [RecordedFuture](https://partners.amazonaws.com/partners/001E000001V9CaHIAV/Recorded%20Future), and are continually updated\. However, AWS Managed Domain Lists aren't intended as a replacement for other security controls, such as Amazon GuardDuty, which are determined by the AWS resources that you select\.

As a best practice, before using a Managed Domain List in production, test it in a non\-production environment, with the rule action set to `Alert`\. Evaluate the rule using Amazon CloudWatch metrics combined with Route 53 Resolver DNS Firewall sampled requests or DNS Firewall logs\. When you're satisfied that the rule does what you want, change the action setting as needed\. 

**Available AWS Managed Domain Lists**  
This section describes the Managed Domain Lists that are currently available\. When you're in a Region where these lists are supported, you see them on the console when you manage domain lists and when you specify the domain list for a rule\. In the logs, the domain list is logged within the `firewall_domain_list_id field`\.

AWS provides the following Managed Domain Lists, in the Regions they are available, for all users of Route 53 Resolver DNS Firewall\. 
+ `AWSManagedDomainsMalwareDomainList` – – Domains associated with sending malware, hosting malware, or distributing malware\.
+ `AWSManagedDomainsBotnetCommandandControl` – Domains associated with controlling networks of computers that are infected with spamming malware\. 
+ `AWSManagedAggregateThreatList` – Domains associated with multiple DNS threat categories including malware, ransomware, botnet, spyware, and DNS tunneling to help block multiple types of threats\. 

AWS Managed Domain Lists cannot be downloaded or browsed\. To protect intellectual property, you can't view or edit the individual domain specifications within an AWS Managed Domain Lists\. This restriction also helps to prevent malicious users from designing threats that specifically to circumvent published lists\. 

**To test the managed domain lists**  
We provide the following set of domains for testing the Managed Domain Lists:

**AWSManagedDomainsBotnetCommandandControl**  
+ controldomain1\.botnetlist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com
+ controldomain2\.botnetlist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com
+ controldomain3\.botnetlist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com

**AWSManagedDomainsMalwareDomainList**  
+ controldomain1\.malwarelist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com
+ controldomain2\.malwarelist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com
+ controldomain3\.malwarelist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com

**AWSManagedDomainsGlobalThreatList**  
+ controldomain1\.globalthreatlist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com
+ controldomain2\.globalthreatlist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com
+ controldomain3\.globalthreatlist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com

**AWSManagedDomainsAggregateThreatList**  
+ controldomain1\.aggregatelist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com
+ controldomain2\.aggregatelist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com
+ controldomain3\.aggregatelist\.firewall\.route53resolver\.us\-east\-1\.amazonaws\.com

These domains will resolve to 1\.2\.3\.4 if they aren't blocked\. If you're using the Managed Domain Lists in a VPC, querying for these domains will return the response that a block action in the rule is set to \(for example NODATA\)\. 

For more information about Managed Domain Lists, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 

The following table lists the Region availability for AWS Managed Domain Lists\.


**Managed Domain List Region availability**  

| Region | Managed Domain Lists available? | 
| --- | --- | 
|  Asia Pacific \(Mumbai\)  |  Yes  | 
|  Asia Pacific \(Seoul\)  |  Yes  | 
| Asia Pacific \(Singapore\) |  Yes  | 
|  Asia Pacific \(Sydney\)  |  Yes  | 
|  Asia Pacific \(Tokyo\)  |  Yes  | 
|  Asia Pacific \(Osaka\) Region  |  Yes  | 
|  Canada \(Central\) Region  |  Yes  | 
|  Europe \(Frankfurt\) Region  |  Yes  | 
|  Europe \(Ireland\) Region  |  Yes  | 
|  Europe \(London\) Region  |  Yes  | 
|  Europe \(Milan\)   |  Yes  | 
|  Europe \(Paris\) Region  |  Yes  | 
|  Europe \(Stockholm\)  |  Yes  | 
|  South America \(São Paulo\)  |  Yes  | 
|  US East \(N\. Virginia\)  |  Yes  | 
|  US East \(Ohio\)  |  Yes  | 
|  US West \(N\. California\)  |  Yes  | 
|  US West \(Oregon\)  |  Yes  | 
|  Asia Pacific \(Jakarta\)   |  Yes  | 
|  Africa \(Cape Town\)   |  Yes  | 
|  China \(Beijing\)   |  Yes  | 
|  China \(Ningxia\)   |  Yes  | 
|  AWS GovCloud \(US\)  |  Yes  | 
|  Asia Pacific \(Hong Kong\)  | Yes | 
|  Middle East \(Bahrain\)  | Yes | 

**Additional security considerations**  
AWS Managed Domain Lists are designed to help protect you from common web threats\. When used in accordance with the documentation, these lists add another layer of security for your applications\. However, the Managed Domain Lists aren't intended as a replacement for other security controls, which are determined by the AWS resources that you select\. To ensure that your resources in AWS are properly protected, see the guidance at [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)\. 

**Mitigating false positive scenarios**  
If you are encountering false\-positive scenarios in rules that use Managed Domain Lists to block queries, perform the following steps: 

1. In the Resolver logs, identify the rule group and managed domain list that are causing the false positive\. You do this by finding the log for the query that DNS Firewall is blocking, but that you want to allow through\. The log record lists the rule group, rule action, and the managed list\. For information about the logs, see [Values that appear in Resolver query logs](resolver-query-logs-format.md)\.

1. Create a new rule in the rule group that explicitly allows the blocked query through\. When you create the rule, you can define your own domain list with just the domain specification that you want to allow\. Follow the guidance for rule group and rule management at [Creating a rule group and rules](resolver-dns-firewall-rule-group-managing.md#resolver-dns-firewall-rule-group-adding)\.

1. Prioritize the new rule inside the rule group so that it runs before the rule that's using the managed list\. To do this, give the new rule a lower numeric priority setting\.

When you have updated your rule group, the new rule will explicitly allow the domain name that you want to allow before the blocking rule runs\. 