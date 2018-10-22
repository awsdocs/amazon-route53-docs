# Creating and Managing Traffic Policies<a name="traffic-policies"></a>


+ [Creating a Traffic Policy](#traffic-policies-creating)
+ [Values that You Specify When You Create a Traffic Policy](#traffic-policies-creating-values)
+ [Creating Additional Versions of a Traffic Policy](#traffic-policies-creating-versions)
+ [Creating a Traffic Policy by Importing a JSON Document](#traffic-policy-import)
+ [Viewing Traffic Policy Versions and the Associated Policy Records](#traffic-policies-viewing)
+ [Deleting Traffic Policy Versions and Traffic Policies](#traffic-policies-deleting)

## Creating a Traffic Policy<a name="traffic-policies-creating"></a>

To create a traffic policy, perform the following procedure\.

**To create a traffic policy**

1. Design your configuration\. For information about how complex DNS routing configurations work, see [Configuring DNS Failover](dns-failover-configuring.md) in [Creating Amazon Route 53 Health Checks and Configuring DNS Failover](dns-failover.md)\.

1. Based on the design for your configuration, create the health checks that you want to use for your endpoints\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Traffic policies**\.

1. Choose **Create traffic policy**\.

1. On the **Name policy** page, specify the applicable values\. For more information, see [Values that You Specify When You Create a Traffic Policy](#traffic-policies-creating-values)\.

1. Choose **Next**\.

1. On the *policy name* page, specify the applicable values\. For more information, see [Values that You Specify When You Create a Traffic Policy](#traffic-policies-creating-values)\.

   You can delete rules, endpoints, and branches of a traffic policy in the following ways:

   + To delete a rule or an endpoint, click the **x** in the upper\-right corner of the box\.
**Important**  
If you delete a rule that has child rules and endpoints, Amazon Route 53 also deletes all of the children\. 

   + If you connect two rules to the same child rule or endpoint and you want to delete one of the connections, pause your cursor on the connection that you want to delete, and click the **x** for that connection\.

1. Choose **Next**\.

1. *Optional*: Specify the settings to create one or more policy records in one hosted zone by using the new traffic policy\. For more information, see [Values that You Specify When You Create or Update a Policy Record](traffic-policy-records.md#traffic-policy-records-creating-values)\. You can also create policy records later, either in the same hosted zone or in additional hosted zones\.

   If you don't want to create policy records now, choose **Skip this step**, and the console displays the list of traffic policies and policy records that you have created by using the current AWS account\.

1. If you specified settings for policy records in the preceding step, choose **Create policy record**\.

## Values that You Specify When You Create a Traffic Policy<a name="traffic-policies-creating-values"></a>

When you create a traffic policy, you specify the following values\.

+ [[ERROR] BAD/MISSING LINK TEXT](#traffic-policies-creating-values-policy-name)

+ [[ERROR] BAD/MISSING LINK TEXT](#traffic-policies-creating-values-version)

+ [[ERROR] BAD/MISSING LINK TEXT](#traffic-policies-creating-values-version-description)

+ [[ERROR] BAD/MISSING LINK TEXT](#traffic-policies-creating-values-dns-type)

+ [[ERROR] BAD/MISSING LINK TEXT](#traffic-policies-creating-values-connect-to)

+ [[ERROR] BAD/MISSING LINK TEXT](#traffic-policies-creating-values-value-type)

+ [[ERROR] BAD/MISSING LINK TEXT](#traffic-policies-creating-values-value)

### Policy name<a name="traffic-policies-creating-values-policy-name"></a>

Enter a name that describes the traffic policy\. This value appears in the list of traffic policies in the console\. You can't change the name of a traffic policy after you create it\.

### Version<a name="traffic-policies-creating-values-version"></a>

This value is assigned automatically by Amazon Route 53 when you create a traffic policy or a new version of an existing policy\.

### Version description<a name="traffic-policies-creating-values-version-description"></a>

Enter a description that applies to this version of the traffic policy\. This value appears in the list of traffic policy versions in the console\.

### DNS type<a name="traffic-policies-creating-values-dns-type"></a>

Choose the DNS type that you want Amazon Route 53 to assign to all of the records when you create a policy record by using this traffic policy version\. For a list of supported types, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

**Important**  
If you're creating a new version of an existing traffic policy, you can change the DNS type\. However, you can't edit a policy record and choose a traffic policy version that has a DNS type that is different from the traffic policy version that you used to create the policy record\. For example, if you created a policy record by using a traffic policy version that has a **DNS type** of A, you can't edit the policy record and choose a traffic policy version that has any other value for **DNS type**\. 

If you want to route traffic to the following AWS resources, choose the applicable value:

+ **CloudFront distribution** – Choose **A: IP address in IPv4 format**\.

+ **ELB load balancer** – Choose either **A: IP address in IPv4 format** or **AAAA: IP address in IPv6 format**\.

+ **Amazon S3 bucket configured as a website endpoint**: Choose **A: IP address in IPv4 format**\.

### Connect to<a name="traffic-policies-creating-values-connect-to"></a>

Choose the applicable rule or endpoint based on the design for your configuration\. 

**Failover rule**  
Choose this option when you want to configure active\-passive failover, in which one resource takes all traffic when it's available and the other resource takes all traffic when the first resource isn't available\.  
For more information, see [Active\-Passive Failover](dns-failover-types.md#dns-failover-types-active-passive)\.

**Geolocation rule**  
Choose this option when you want Amazon Route 53 to respond to DNS queries based on the location of your users\.  
For more information, see [Geolocation Routing](routing-policy.md#routing-policy-geo)\.  
When you choose **Geolocation rule**, you also choose the country or the state in the United States that requests originate from\.

**Latency rule**  
Choose this option when you have resources in multiple Amazon EC2 data centers that perform the same function, and you want Route 53 to respond to DNS queries with the resources that provide the best latency\.  
When you choose **Latency rule**, you also choose an AWS Region\.  
For more information, see [Latency\-based Routing](routing-policy.md#routing-policy-latency)\.

**Geoproximity rule**  
Choose this option when you want Route 53 to respond to DNS queries based on the location of your resources and optionally on a bias that you specify\. The bias allows you to send more traffic to a resource or more traffic away from a resource\.  
When you choose **Geoproximity rule**, enter the following values:    
**Endpoint location**  
Choose the applicable value:  

+ **Custom \(enter coordinates\)** – If your endpoint is not an AWS resource, choose **Custom \(enter coordinates\)**\.

+ **An AWS Region** – If your endpoint is an AWS resource, choose the AWS Region that you created the resource in\.  
**Coordinates**  
If you chose **Custom \(enter coordinates\)** for **Endpoint location**, enter the latitude and longitude of the location of the resource\. Note the following:  

+ Latitude represents the location south \(negative\) or north \(positive\) of the equator\. Valid values are \-90 degrees to 90 degrees\.

+ Longitude represents the location west \(negative\) or east \(positive\) of the prime meridian\. Valid values are \-180 degrees to 180 degrees\.

+ You can get latitude and longitude from some online mapping applications\. For example, in Google Maps, the URL for a location specifies the latitude and longitude:

  https://www\.google\.com/maps/@**47\.6086111**,\-**122\.3409953**,20z

+ You can enter up to two decimals of precision, for example, **47\.63**\. If you specify a value with greater precision, Route 53 truncates the value to two places after the decimal\. For latitude and for longitude at the equator, 0\.01 degree is approximately 0\.69 miles\.  
**Bias**  
Specify a value for **Bias** if you want to route more traffic to an endpoint from nearby endpoints \(positive values\) or route less traffic to an endpoint \(negative values\)\. The range of valid values is \-99 to 99; the default value is 0\.  
The value of **Bias** is relative, based on the location of other resources, rather than absolute, based on distance\. As a result, the effect of a change is difficult to predict\. For example, depending on where your resources are, changing the bias from 10 to 15 can mean the difference between adding or subtracting a significant amount of traffic from the New York City metropolitan area\. We recommend that you change the bias in small increments and evaluate the results, and then make additional changes if appropriate\.
For more information, see [Geoproximity Routing \(Traffic Flow Only\)](routing-policy.md#routing-policy-geoproximity)\.

**Multivalue answer rule**  
Choose this option when you want Route 53 to respond to DNS queries with up to eight healthy answers selected approximately at random\.   
For more information, see [Multivalue Answer Routing](routing-policy.md#routing-policy-multivalue)\.

**Weighted rule**  
Choose this option when you have multiple resources that perform the same function \(for example, web servers that serve the same website\) and you want Route 53 to route traffic to those resources in proportions that you specify \(for example, 1/3rd to one server and 2/3rds to the other\)\.  
When you choose **Weighted rule**, enter the weight that you want to apply to this rule\.  
For more information, see [Weighted Routing](routing-policy.md#routing-policy-weighted)\.

**Endpoint**  
Choose this option to specify the resource, such as a CloudFront distribution or an ELB load balancer, that you want to route DNS queries to\.

**Existing rule**  
Choose this option when you want to route DNS queries to an existing rule in this traffic policy\. For example, you might create two or more geolocation rules that route queries for different countries to the same failover rule\. The failover rule might then routes queries to two ELB load balancers\.  
This option isn't available if the traffic policy doesn't include any rules\.

**Existing endpoint**  
Choose this option when you want to route DNS queries to an existing endpoint\. For example, if you have two failover rules, you might want to route DNS queries for both **On failover** \(secondary\) options to the same ELB load balancer\.  
This option isn't available if the traffic policy doesn't include any endpoints\.

### Value type<a name="traffic-policies-creating-values-value-type"></a>

Choose the applicable option:

**CloudFront distribution**  
Choose this option if you want to route traffic to a CloudFront distribution\. The option is available only if you chose **A: IP address in IPv4 format** for **DNS type**\. 

**ELB load balancer**  
Choose this option if you want to route traffic to an ELB load balancer\. The option is available only if you chose either **A: IP address in IPv4 format** or **AAAA: IP address in IPv6 format** for **DNS type**\. 

**S3 website endpoint**  
Choose this option if you want to route traffic to an Amazon S3 bucket that is configured as a website endpoint\. The option is available only if you chose **A: IP address in IPv4 format** for **DNS type**\. 

**Type *DNS type* value**  
Choose this option if you want Route 53 to respond to DNS queries using the value in the **Value** field\. For example, if you chose **A** for the value of **DNS type** when you created this traffic policy, this option in the **Value type** list will be **Type A value**\. This requires that you enter an IP address in IPv4 format in the **Value** field\. Route 53 will respond to DNS queries that are routed to this endpoint with the IP address in the **Value** field\.

### Value<a name="traffic-policies-creating-values-value"></a>

Choose or enter a value based on the option that you chose for **Value type**:

**CloudFront distribution**  
Choose a CloudFront distribution from the list of distributions that are associated with the current AWS account\.

**ELB load balancer**  
Choose an ELB load balancer from the list of ELB load balancers that are associated with the current AWS account\.

**S3 website endpoint**  
Choose an Amazon S3 bucket from the list of Amazon S3 buckets that are configured as website endpoints and that are associated with the current AWS account\.  
When you create a policy record based on this traffic policy, the bucket that you choose here must match the domain name \(such as www\.example\.com\) that you specify for [Policy record DNS name](traffic-policy-records.md#traffic-policy-records-creating-values-policy-record-dns-name) in the policy record\. If **Value** and **Policy record DNS name** don't match, Amazon S3 won't respond to DNS queries for the domain name\.

**Type *DNS type* value**  
Enter a value that corresponds with the value that you specified for **DNS type** when you started this traffic policy\. For example, if you chose **MX** for **DNS type**, enter two values: the priority that you want to assign to a mail server and the domain name of the mail server, such as `10 sydney.mail.example.com`\.  
For more information about supported DNS types, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

## Creating Additional Versions of a Traffic Policy<a name="traffic-policies-creating-versions"></a>

When you edit a traffic policy, Amazon Route 53 automatically creates another version of the traffic policy and retains the previous versions unless you choose to delete them\. The new version has the same name as the traffic policy that you're editing; it's distinguished from the original version by a version number that Route 53 increments automatically\. You can base the new version of a traffic policy on any existing version of a traffic policy that has the same name\.

Route 53 doesn't reuse version numbers for new versions of a given traffic policy\. For example, if you create three versions of **MyTrafficPolicy**, delete the last two versions, and then create another version, the new version is version 4\. By retaining the previous versions, Route 53 ensures that you can roll back to a previous configuration if a new configuration doesn't route traffic as you wanted it to\. 

To create a new traffic policy version, perform the following procedure\.

**To create another version of a traffic policy**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Traffic policies**\.

1. Choose the name of the traffic policy that you want to create a new version of\.

1. In the **Traffic policy versions** table at the top of the page, select the check box for the traffic policy version that you want to use as a basis for the new traffic policy version\.

1. Choose **Edit policy as new version**\.

1. On the **Update description** page, enter a description for the new traffic policy version\. We recommend that you specify a description that distinguishes this version from other versions of the same traffic policy\. When you create a new policy record, the value that you specify appears in the list of available versions for this traffic policy\.

1. Choose **Next**\.

1. Update the configuration as applicable\. For more information, see [Values that You Specify When You Create a Traffic Policy](#traffic-policies-creating-values)\.

   You can delete rules, endpoints, and branches of a traffic policy in the following ways:

   + To delete a rule or an endpoint, click the **x** in the upper\-right corner of the box\.
**Important**  
If you delete a rule that has child rules and endpoints, Route 53 also deletes all of the children\. 

   + If you connect two rules to the same child rule or endpoint and you want to delete one of the connections, pause your cursor on the connection that you want to delete, and click the **x** for that connection\.

1. When you're finished editing, choose **Save as new version**\.

1. *Optional*: Specify the settings to create one or more policy records in one hosted zone by using the new traffic policy version\. For more information, see [Values that You Specify When You Create or Update a Policy Record](traffic-policy-records.md#traffic-policy-records-creating-values)\. You can also create policy records later, either in the same hosted zone or in additional hosted zones\.

   If you don't want to create policy records now, choose **Skip this step**, and the console displays the list of traffic policies and policy records that you have created by using the current AWS account\.

1. If you specified settings for policy records in the preceding step, choose **Create policy record**\.

## Creating a Traffic Policy by Importing a JSON Document<a name="traffic-policy-import"></a>

You can create a new traffic policy or a new version of an existing traffic policy by importing a document in JSON format that describes all of the endpoints and rules that you want to include in the traffic policy\. For information about the format of the JSON document and several examples that you can copy and revise, see [Traffic Policy Document Format](http://docs.aws.amazon.com/Route53/latest/APIReference/api-policies-traffic-policy-document-format.html) in the *Amazon Route 53 API Reference*\.

The easiest way to get the JSON\-formatted document for an existing traffic policy version is to use the `get-traffic-policy` command in the AWS CLI\. For more information, see [get\-traffic\-policy](http://docs.aws.amazon.com/cli/latest/reference/route53/get-traffic-policy.html) in the *AWS CLI Command Reference*\. 

**To create a traffic policy by importing a JSON document**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. To create a new traffic policy by importing a JSON document, perform the following steps:

   1. In the navigation pane, choose **Traffic policies**\.

   1. Choose **Create traffic policy**\.

   1. On the **Name policy** page, specify the applicable values\. For more information, see [Values that You Specify When You Create a Traffic Policy](#traffic-policies-creating-values)\.

   1. Skip to step 4\.

1. To create a new version of an existing traffic policy by importing a JSON document, perform the following steps:

   1. In the navigation pane, choose **Traffic policies**\.

   1. Choose the name of the traffic policy that you want to base the new version on\. 

   1. In the **Traffic policy versions** table, select the check box for the version that you want to base the new version on\.

   1. Choose **Edit policy as new version**\.

   1. On the **Update description** page, enter a description for the new version\.

   1. Skip to step 4\.

1. Choose **Next**\.

1. Choose **Import traffic policy**\.

1. Enter a new traffic policy, paste an example traffic policy, or paste an existing traffic policy\. 

1. Choose **Import traffic policy**\.

## Viewing Traffic Policy Versions and the Associated Policy Records<a name="traffic-policies-viewing"></a>

You can view all of the versions that you've created for a traffic policy as well as all of the policy records that you've created by using each of the versions of the traffic policy\.

**To view traffic policy versions and the associated policy records**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Traffic policies**\.

1. Choose the name of a traffic policy\.

1. The top table lists all of the versions that you've created of a traffic policy\. The table includes the following information:  
**Version number**  
The number of each version of a traffic policy that you've created\. If you choose the version number, the console displays the configuration for that version\.  
**Number of policy records**  
The number of policy records that you've created by using this traffic policy version\.  
**DNS type**  
The DNS type that you specified when you created the traffic policy version\.  
**Version description**  
The description that you specified when you created the traffic policy version\.

1. The bottom table lists all of the policy records that you've created by using the traffic policy versions in the top table\. The table includes the following information:  
**Policy record DNS name**  
The DNS names that you've associated the traffic policy with\.  
**Status**  
Possible values include the following:    
**Applied**  
Route 53 has finished creating or updating a policy record and the corresponding records\.  
**Creating**  
Route 53 is creating the records for a new policy record\.  
**Updating**  
You have updated a policy record and Route 53 is in the process of creating a new group of records that will replace the existing group of records for the specified DNS name\.  
**Deleting**  
Route 53 is in the process of deleting a policy record and the associated records\.  
**Failed**  
Route 53 wasn't able to create or update the policy record and the associated records\.   
**Version used**  
Indicates the version of the traffic policy that you used to create the policy record\.  
**DNS type**  
The DNS type of all of the records that Route 53 created for this policy record\. When you edit a policy record, you must specify a traffic policy version that has the same DNS type as the DNS type for the policy record that you're editing\.  
**TTL \(in seconds\)**  
The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this record\. If you specify a longer value \(for example, 172800 seconds, or two days\), you pay less for Route 53 service because recursive resolvers send requests to Route 53 less often\. However, it takes longer for changes to the records \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods instead of asking Route 53 for the latest information\.

## Deleting Traffic Policy Versions and Traffic Policies<a name="traffic-policies-deleting"></a>

To delete a traffic policy, you must delete all of the versions \(including the original\) that you've created for the traffic policy\. In addition, to delete a traffic policy version, you must delete all of the policy records that you created by using the traffic policy version\.

**Important**  
If you delete policy records that Amazon Route 53 is using to respond to DNS queries, Route 53 will stop responding to queries for the corresponding DNS names\. For example, if Route 53 is using the policy record for www\.example\.com to respond to DNS queries for www\.example\.com and you delete the policy record, your users will not be able to access your website or web application by using the domain name www\.example\.com\. 

To delete traffic policy versions and, optionally, a traffic policy, perform the following procedure:

**To delete traffic policy versions and a traffic policy**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Traffic policies**\.

1. Choose the name of the traffic policy for which you want to delete traffic policy versions and that, optionally, you want to delete completely\.

1. If the traffic policy versions that you want to delete in the top table appear in the **Version used** column in the bottom table, select the check boxes for the corresponding policy records in the bottom table\. 

   For example, if you want to delete version 3 of a traffic policy but you created one of the policy records in the bottom table by using version 3, select the check box for that policy record\. 

1. Choose **Delete policy records**\.

1. Choose the refresh button for the bottom table to refresh the display until the policy records that you deleted no longer appear in the table\.

1. In the top table, select the check boxes for the traffic policy versions that you want to delete\. 

1. Choose **Delete version**\.

1. If you deleted all traffic policy versions in the preceding step and you want to delete the traffic policy, too, choose the refresh button for the top table to refresh the display until the table is empty\.

1. In the navigation pane, choose **Traffic policies**\. 

1. In the list of traffic policies, select the check box for the traffic policy that you want to delete\.

1. Choose **Delete traffic policy**\.