# Managing Inbound Endpoints<a name="resolver-forwarding-inbound-queries-managing"></a>

To manage inbound endpoints, perform the applicable procedure\.

**Topics**
+ [Viewing and Editing Inbound Endpoints](#resolver-forwarding-inbound-queries-managing-viewing)
+ [Deleting Inbound Endpoints](#resolver-forwarding-inbound-queries-managing-deleting)

## Viewing and Editing Inbound Endpoints<a name="resolver-forwarding-inbound-queries-managing-viewing"></a>

To view and edit settings for an inbound endpoint, perform the following procedure\.<a name="resolver-forwarding-inbound-queries-managing-viewing-procedure"></a>

**To view and edit settings for an inbound endpoint**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Inbound endpoints**\.

1. On the navigation bar, choose the Region where you created the inbound endpoint\.

1. Choose the option for the endpoint that you want to view settings for or want to edit\.

1. Choose **View details** or **Edit**\.

   For information about the values for inbound endpoints, see [Values That You Specify When You Create or Edit Inbound Endpoints](resolver-forwarding-inbound-queries.md#resolver-forwarding-inbound-queries-values)\.

1. If you chose **Edit**, enter the applicable values, and choose **Save**\.

## Deleting Inbound Endpoints<a name="resolver-forwarding-inbound-queries-managing-deleting"></a>

To delete an inbound endpoint, perform the following procedure\.

**Important**  
If you delete an inbound endpoint, DNS queries from your network are no longer forwarded to Resolver in the VPC that you specified in the endpoint\. <a name="resolver-forwarding-inbound-queries-managing-deleting-procedure"></a>

**To delete an inbound endpoint**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Inbound endpoints**\.

1. On the navigation bar, choose the Region where you created the inbound endpoint\.

1. Choose the option for the endpoint that you want to delete\.

1. Choose **Delete**\.

1. To confirm that you want to delete the endpoint, enter the name of the endpoint and choose **Submit**\.