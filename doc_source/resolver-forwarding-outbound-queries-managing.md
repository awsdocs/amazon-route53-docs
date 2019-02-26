# Managing Outbound Endpoints<a name="resolver-forwarding-outbound-queries-managing"></a>

To manage outbound endpoints, perform the applicable procedure\.

**Topics**
+ [Viewing and Editing Outbound Endpoints](#resolver-forwarding-outbound-queries-managing-viewing)
+ [Deleting Outbound Endpoints](#resolver-forwarding-outbound-queries-managing-deleting)

## Viewing and Editing Outbound Endpoints<a name="resolver-forwarding-outbound-queries-managing-viewing"></a>

To view and edit settings for an outbound endpoint, perform the following procedure\.<a name="resolver-forwarding-outbound-queries-managing-viewing-procedure"></a>

**To view and edit settings for an outbound endpoint**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Outbound endpoints**\.

1. On the navigation bar, choose the Region where you created the outbound endpoint\.

1. Choose the option for the endpoint that you want to view settings for or want to edit\.

1. Choose **View details** or **Edit**\.

   For information about the values for inbound endpoints, see [Values That You Specify When You Create or Edit Outbound Endpoints](resolver-forwarding-outbound-queries.md#resolver-forwarding-outbound-queries-endpoint-values)\.

1. If you chose **Edit**, enter the applicable values, and then choose **Save**\.

## Deleting Outbound Endpoints<a name="resolver-forwarding-outbound-queries-managing-deleting"></a>

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