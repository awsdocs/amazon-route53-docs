# Outbound endpoints<a name="resolver-page-outbound-endpoints-list"></a>

To view and update settings for an outbound endpoint, choose the ID of the endpoint\.

Valid values for the **Status** column include the following:
+ **Creating**: Resolver is creating and configuring one or more Amazon VPC network interfaces for this endpoint\.
+ **Operational**: The Amazon VPC network interfaces for this endpoint are correctly configured and able to pass inbound or outbound DNS queries between your network and Resolver\.
+ **Updating**: Resolver is associating or disassociating one or more network interfaces with this endpoint\.
+ **Auto recovering**: Resolver is trying to recover one or more of the network interfaces that are associated with this endpoint\. During the recovery process, the endpoint functions with limited capacity because of the maximum number of DNS queries per IP address \(per network interface\)\. For the current maximum, see [Quotas on Route 53 Resolver](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/DNSLimitations.html#)\.
+ **Action needed**: This endpoint is unhealthy, and Resolver can't automatically recover it\. To resolve the problem, we recommend that you check each IP address that you associated with the endpoint\. For each IP address that isn't available, add another IP address and then delete the IP address that isn't available\. \(An endpoint must always include at least two IP addresses\.\) A status of **Action needed** can have a variety of causes\. Here are two common causes:
  + One or more of the network interfaces that are associated with the endpoint were deleted using Amazon VPC\.
  + The network interface couldn't be created for some reason that's outside the control of Resolver\.
+ **Deleting**: Resolver is deleting this endpoint and the associated network interfaces\.

## Learn more<a name="resolver-page-outbound-endpoints-list-learn-more"></a>
+ [Managing outbound endpoints](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-forwarding-outbound-queries-managing.html)