# Managing outbound endpoints<a name="resolver-forwarding-outbound-queries-managing"></a>

To manage outbound endpoints, perform the applicable procedure\.

**Topics**
+ [Viewing and editing outbound endpoints](#resolver-forwarding-outbound-queries-managing-viewing)
+ [Viewing the status for outbound endpoints](#resolver-forwarding-outbound-queries-managing-viewing-status)
+ [Deleting outbound endpoints](#resolver-forwarding-outbound-queries-managing-deleting)

## Viewing and editing outbound endpoints<a name="resolver-forwarding-outbound-queries-managing-viewing"></a>

To view and edit settings for an outbound endpoint, perform the following procedure\.<a name="resolver-forwarding-outbound-queries-managing-viewing-procedure"></a>

**To view and edit settings for an outbound endpoint**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Outbound endpoints**\.

1. On the navigation bar, choose the Region where you created the outbound endpoint\.

1. Choose the option for the endpoint that you want to view settings for or want to edit\.

1. Choose **View details** or **Edit**\.

   For information about the values for outbound endpoints, see [Values that you specify when you create or edit outbound endpoints](resolver-forwarding-outbound-queries.md#resolver-forwarding-outbound-queries-endpoint-values)\.

1. If you chose **Edit**, enter the applicable values, and then choose **Save**\.

## Viewing the status for outbound endpoints<a name="resolver-forwarding-outbound-queries-managing-viewing-status"></a>

To view the status for an outbound endpoint, perform the following procedure\.<a name="resolver-forwarding-outbound-queries-managing-viewing-status-procedure"></a>

**To view the status for an outbound endpoint**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Outbound endpoints**\.

1. On the navigation bar, choose the Region where you created the outbound endpoint\. The **Status** column contains one of the following values:  
**Creating**  
Resolver is creating and configuring one or more Amazon VPC network interfaces for this endpoint\.  
**Operational**  
The Amazon VPC network interfaces for this endpoint are correctly configured and able to pass inbound or outbound DNS queries between your network and Resolver\.  
**Updating**  
Resolver is associating or disassociating one or more network interfaces with this endpoint\.  
**Auto recovering**  
Resolver is trying to recover one or more of the network interfaces that are associated with this endpoint\. During the recovery process, the endpoint functions with limited capacity because of the limit on the number of DNS queries per IP address \(per network interface\)\. For the current limit, see [Quotas on Route 53 Resolver](DNSLimitations.md#limits-api-entities-resolver)\.  
**Action needed**  
This endpoint is unhealthy, and Resolver can't automatically recover it\. To resolve the problem, we recommend that you check each IP address that you associated with the endpoint\. For each IP address that isn't available, add another IP address and then delete the IP address that isn't available\. \(An endpoint must always include at least two IP addresses\.\) A status of **Action needed** can have a variety of causes\. Here are two common causes:  
   + One or more of the network interfaces that are associated with the endpoint were deleted using Amazon VPC\.
   + The network interface couldn't be created for some reason that's outside the control of Resolver\.  
**Deleting**  
Resolver is deleting this endpoint and the associated network interfaces\.

## Deleting outbound endpoints<a name="resolver-forwarding-outbound-queries-managing-deleting"></a>

To delete an outbound endpoint, perform the following procedure\.

**Important**  
If you delete an outbound endpoint, Resolver stops forwarding DNS queries from your VPC to your network for rules that specify the deleted outbound endpoint\.<a name="resolver-forwarding-outbound-queries-managing-deleting-procedure"></a>

**To delete an outbound endpoint**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Outbound endpoints**\.

1. On the navigation bar, choose the Region where you created the outbound endpoint\.

1. Choose the option for the endpoint that you want to delete\.

1. Choose **Delete**\.

1. To confirm that you want to delete the endpoint, enter the name of the endpoint, and then choose **Submit**\.