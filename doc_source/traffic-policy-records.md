# Creating and Managing Policy Records<a name="traffic-policy-records"></a>

You create policy records to apply the configuration that you created in a traffic policy to one or more domain names or subdomain names\.

**Topics**
+ [Creating Policy Records](#traffic-policy-records-creating)
+ [Values that You Specify When You Create or Update a Policy Record](#traffic-policy-records-creating-values)
+ [Updating Policy Records](#traffic-policy-records-updating)
+ [Deleting Policy Records](#traffic-policy-records-deleting)

## Creating Policy Records<a name="traffic-policy-records-creating"></a>

To create a policy record, perform the following procedure\.

**Important**  
For each policy record that you create, you incur a monthly charge\. If you later delete the policy record, the charge is prorated\. For more information, see [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.<a name="traffic-policy-records-creating-procedure"></a>

**To create a policy record**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Policy records**\.

1. On the **Policy records** page, choose **Create policy records**\.

1. On the **Create policy records** page, specify the applicable values\. For more information, see [Values that You Specify When You Create or Update a Policy Record](#traffic-policy-records-creating-values)\.

1. Choose **Create policy records**\.

1. If you want to create policy records in another hosted zone, repeat steps 3 through 5\.

## Values that You Specify When You Create or Update a Policy Record<a name="traffic-policy-records-creating-values"></a>

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

## Updating Policy Records<a name="traffic-policy-records-updating"></a>

To update the settings in a policy record, perform the following procedure\. <a name="traffic-policy-records-updating-procedure"></a>

**To update a policy record**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Policy records**\.

1. On the **Policy records** page, select the check box for the policy record that you want to update, and choose **Edit policy record**\. 

1. On the **Edit policy record** page, specify the applicable values\. For more information, see [Values that You Specify When You Create or Update a Policy Record](#traffic-policy-records-creating-values)\.

1. Choose **Edit policy record**\.

1. If you want to update another policy record, repeat steps 3 through 5\.

## Deleting Policy Records<a name="traffic-policy-records-deleting"></a>

To delete policy records, perform the following procedure\.

**Important**  
If you delete policy records that Amazon Route 53 is using to respond to DNS queries, Route 53 will stop responding to queries for the corresponding DNS names\. For example, if Route 53 is using the policy record for www\.example\.com to respond to DNS queries for www\.example\.com and you delete the policy record, your users will not be able to access your website or web application by using the domain name www\.example\.com\. <a name="traffic-policy-records-deleting-procedure"></a>

**To delete a policy record**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Policy records**\.

1. On the **Policy records** page, select the check boxes for the policy records that you want to delete, and choose **Delete policy record**\. 