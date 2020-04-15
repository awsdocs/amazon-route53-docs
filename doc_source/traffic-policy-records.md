# Creating and managing policy records<a name="traffic-policy-records"></a>

To route internet traffic to the resources that you specified when you created a [traffic policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/traffic-policies.html), you create one or more policy records\. Each policy record identifies the hosted zone where you want to create the policy record and the domain or subdomain name that you want to route traffic for\. For example, if you want to route traffic for www\.example\.com, you specify the hosted zone ID for the example\.com hosted zone, and you specify www\.example\.com for the **Policy record DNS name**\.

If you want to use the same traffic policy to route traffic for more than one domain or subdomain name, you have two options:
+ You can create a policy record for each domain or subdomain name\.
+ You can create one policy record and then create CNAME or alias records that refer to the policy record\.

For example, if you want to use the same traffic policy for example\.com, example\.net, and example\.org, you can do either of the following:
+ Create one policy record for each of them\.
+ Create a policy record for one of them and then create CNAME records in the hosted zones for the other two\. In the two CNAME records, you specify the record name that you created a policy record for\.

If you want to use the same traffic policy for a domain and its subdomains, such as example\.com and www\.example\.com, you can create a policy record for one name and then create alias records for the rest\. For example, you can create a policy record for example\.com and then create an alias record for www\.example\.com that has the example\.com record as the alias target\.

**Note**  
There's a monthly charge for each policy record that you create\. If you want to use the same traffic policy for multiple domain or subdomain names, you can use CNAME or alias records to reduce your charges:  
If you create one policy record and one or more CNAME records that refer to the policy record, you pay only for the policy record and for DNS queries for the CNAME records\.
If you create one policy record and one or more alias records in the same hosted zone that refer to the policy record, you pay only for the policy record and for DNS queries for the alias records\.

**Topics**
+ [Creating policy records](#traffic-policy-records-creating)
+ [Values that you specify when you create or update a policy record](#traffic-policy-records-creating-values)
+ [Updating policy records](#traffic-policy-records-updating)
+ [Deleting policy records](#traffic-policy-records-deleting)

## Creating policy records<a name="traffic-policy-records-creating"></a>

To create a policy record, perform the following procedure\.

**Important**  
For each policy record that you create, you incur a monthly charge\. If you later delete the policy record, the charge is prorated\. For more information, see the section "Traffic Flow" on the [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/) page\.<a name="traffic-policy-records-creating-procedure"></a>

**To create a policy record**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Policy records**\.

1. On the **Policy records** page, choose **Create policy records**\.

1. On the **Create policy records** page, specify the applicable values\. For more information, see [Values that you specify when you create or update a policy record](#traffic-policy-records-creating-values)\.

1. Choose **Create policy records**\.

1. If you want to create policy records in another hosted zone, repeat steps 3 through 5\.

## Values that you specify when you create or update a policy record<a name="traffic-policy-records-creating-values"></a>

When you create or update a policy record, you specify the following values
+ [Traffic policy](#traffic-policy-records-creating-values-traffic-policy)
+ [Version](#traffic-policy-records-creating-values-version)
+ [Hosted zone](#traffic-policy-records-creating-values-hosted-zone)
+ [Policy record DNS name](#traffic-policy-records-creating-values-policy-record-dns-name)
+ [TTL](#traffic-policy-records-creating-values-ttl)

**Traffic policy**  
Choose the traffic policy whose configuration you want to use for this policy record\.

**Version**  
Choose the version of the traffic policy whose configuration you want to use for this policy record\.  
If you're updating an existing policy record, you must choose a version for which the DNS type matches the current DNS type of the policy record\. For example, if the DNS type of the policy record is **A**, you must choose a version for which the DNS type is **A**\.

**Hosted zone**  
Choose the hosted zone in which you want to create a policy record by using the specified traffic policy and version\. You can't change the value of **Hosted zone** after you create a policy record\. 

**Policy record DNS name**  
When you're creating a policy record, enter the domain name or subdomain name for which you want Route 53 to respond to DNS queries by using the configuration in the specified traffic policy and version\.   
To use the same configuration for more than one domain name or subdomain name in the specified hosted zone, choose **Add another policy record**, and enter the applicable domain name or subdomain name and TTL\.  
You can't change the value of **Policy record DNS name** after you create a policy record\.

**TTL \(in seconds\)**  
Enter the amount of time, in seconds, that you want DNS recursive resolvers to cache information about this record\. If you specify a longer value \(for example, 172800 seconds, or two days\), you pay less for Route 53 service because recursive resolvers send requests to Route 53 less often\. However, it takes longer for changes to the records \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods instead of asking Route 53 for the latest information\. 

## Updating policy records<a name="traffic-policy-records-updating"></a>

To update the settings in a policy record, perform the following procedure\. <a name="traffic-policy-records-updating-procedure"></a>

**To update a policy record**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Policy records**\.

1. On the **Policy records** page, select the check box for the policy record that you want to update, and choose **Edit policy record**\. 

1. On the **Edit policy record** page, specify the applicable values\. For more information, see [Values that you specify when you create or update a policy record](#traffic-policy-records-creating-values)\.

1. Choose **Edit policy record**\.

1. If you want to update another policy record, repeat steps 3 through 5\.

## Deleting policy records<a name="traffic-policy-records-deleting"></a>

To delete policy records, perform the following procedure\.

**Important**  
If you delete policy records that Amazon Route 53 is using to respond to DNS queries, Route 53 will stop responding to queries for the corresponding DNS names\. For example, if Route 53 is using the policy record for www\.example\.com to respond to DNS queries for www\.example\.com and you delete the policy record, your users will not be able to access your website or web application by using the domain name www\.example\.com\. <a name="traffic-policy-records-deleting-procedure"></a>

**To delete a policy record**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Policy records**\.

1. On the **Policy records** page, select the check boxes for the policy records that you want to delete, and choose **Delete policy record**\. 