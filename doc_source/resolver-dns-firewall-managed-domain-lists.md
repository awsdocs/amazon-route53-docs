# Managed domain lists<a name="resolver-dns-firewall-managed-domain-lists"></a>

Managed domain lists contain domain names that are associated with malicious activity or other potential threats\. AWS maintains these lists to enable Route 53 Resolver customers to check outbound DNS queries against them for free when using DNS Firewall\. 

Keeping up to date on the constantly changing threat landscape can be time consuming and expensive\. Managed domain lists can save you time when you implement and use DNS Firewall\. AWS automatically updates managed domain lists when as new vulnerabilities and threats emerge\. AWS is often notified of new vulnerabilities before public disclosure, so DNS Firewall can deploy mitigations for you even, often before a new threats is become widely known\. 

AWS Managed Domain Lists are designed to help protect you from common web threats and they add another layer of security for your applications\. However, AWS Managed Domain Lists aren't intended as a replacement for other security controls, such as Amazon GuardDuty, which are determined by the AWS resources that you select\.

AWS Managed Domain Lists are not currently available in all Regions\. The following table lists the Region availability\.


**Managed domain list Region availability**  

| Region | Managed domain lists available? | 
| --- | --- | 
|  Asia Pacific \(Mumbai\)  |  Yes  | 
|  Asia Pacific \(Seoul\)  |  Yes  | 
| Asia Pacific \(Singapore\) |  Yes  | 
|  Asia Pacific \(Sydney\)  |  Yes  | 
|  Asia Pacific \(Tokyo\)  |  Yes  | 
| Asia Pacific \(Osaka\) Region  |  Yes  | 
|  Canada \(Central\) Region  |  Yes  | 
|  Europe \(Frankfurt\) Region  |  Yes  | 
|  Europe \(Ireland\) Region  |  Yes  | 
|  Europe \(London\) Region  |  Yes  | 
|  Europe \(Paris\) Region  |  Yes  | 
|  Europe \(Stockholm\)  |  Yes  | 
|  South America \(São Paulo\)  |  Yes  | 
|  US East \(N\. Virginia\)  |  Yes  | 
|  US East \(Ohio\)  |  Yes  | 
|  US West \(N\. California\)  |  Yes  | 
|  US West \(Oregon\)  |  Yes  | 
|  AWS GovCloud \(US\)  |  No  | 
|  Asia Pacific \(Hong Kong\)  |  No  | 
|  Middle East \(Bahrain\)  |  No  | 
|  Africa \(Cape Town\)   |  No  | 
|  Europe \(Milan\)   |  No  | 
|  Asia Pacific \(Jakarta\)   |  No  | 
|  China \(Beijing\)   |  No  | 
|  China \(Ningxia\)   |  No  | 

**Available AWS Managed Domain Lists**  
This section describes the AWS Managed Domain Lists that are currently available\. When you're in a Region where these domain lists are supported, you see them on the console when you manage domain lists and when you specify the domain list for a rule\. In the logs, the domain list is logged within the `firewall_domain_list_id field`\.

AWS provides the following managed domain lists, in the Regions they are available, for all users of Route 53 Resolver DNS Firewall\. 
+ `AWSManagedDomainsMalwareDomainList` – – Domains associated with sending malware, hosting malware, or distributing malware\.
+ `AWSManagedDomainsBotnetCommandandControl` – Domains associated with controlling networks of computers that are infected with spamming malware\. 

Managed domain lists cannot be downloaded or browsed\. To protect intellectual property, you can't view or edit the individual domain specifications within a domain list\. This restriction also helps to prevent malicious users from designing threats that specifically to circumvent published lists\. 

For more information about managed domain lists, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 

As a best practice, before using a managed domain list in production, test it in a non\-production environment, with the rule action set to `Alert`\. Evaluate the rule using Amazon CloudWatch metrics combined with Route 53 Resolver DNS Firewall sampled requests or DNS Firewall logs\. When you're satisfied that the rule does what you want, change the action setting as needed\. 

**Additional security considerations**  
AWS Managed Domain Lists are designed to help protect you from common web threats\. When used in accordance with the documentation, AWS Managed Domain Lists add another layer of security for your applications\. However, AWS Managed Domain Lists aren't intended as a replacement for other security controls, which are determined by the AWS resources that you select\. To ensure that your resources in AWS are properly protected, see the guidance at [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)\. 

**Mitigating false positive scenarios**  
If you are encountering false\-positive scenarios in rules that use AWS Managed Domain Lists to block queries, perform the following steps: 

1. In the Resolver logs, identify the rule group and managed domain list that are causing the false positive\. You do this by finding the log for the query that DNS Firewall is blocking, but that you want to allow through\. The log record lists the rule group, rule action, and the managed domain list\. For information about the logs, see [Values that appear in Resolver query logs](resolver-query-logs-format.md)\.

1. Create a new rule in the rule group that explicitly allows the blocked query through\. When you create the rule, you can define your own domain list with just the domain specification that you want to allow\. Follow the guidance for rule group and rule management at [Creating a rule group and rules](resolver-dns-firewall-rule-group-managing.md#resolver-dns-firewall-rule-group-adding)\.

1. Prioritize the new rule inside the rule group so that it runs before the rule that's using the managed domain list\. To do this, give the new rule a lower numeric priority setting\.

When you have updated your rule group, the new rule will explicitly allow the domain name that you want to allow before the blocking rule runs\. 