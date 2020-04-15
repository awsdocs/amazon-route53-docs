# Task list for configuring DNS failover<a name="dns-failover-how-to"></a>

To use Route 53 to configure DNS failover, perform the following tasks:

1. Draw a complete tree diagram of your configuration, and indicate which type of record you're creating \(weighted alias, failover, latency, and so on\) for each node\. At the top of the tree put the records for the domain name, such as example\.com, that your users will use to access your website or web application\.

   The kinds of records that appear in your tree diagram depend on the complexity of the configuration:
   + In a simple configuration, either your diagram won't include any alias records, or the alias records will route traffic directly to a resource, such as an ELB load balancer, instead of to another Route 53 record\. For more information, see [How health checks work in simple Amazon Route 53 configurationsHow health checks work in simple configurations](dns-failover-simple-configs.md)\.
   + In a complex configuration, your diagram will include a combination of alias records \(such as weighted alias and failover alias\) and non\-alias records in a multi\-level tree like the examples in the topic [How health checks work in complex Amazon Route 53 configurationsHow health checks work in complex configurations](dns-failover-complex-configs.md)\.
**Note**  
To quickly and easily create records for complex routing configurations and associate the records with health checks, you can use the traffic flow visual editor and save the configuration as a traffic policy\. You can then associate the traffic policy with one or more domain names \(such as example\.com\) or subdomain names \(such as www\.example\.com\), in the same hosted zone or in multiple hosted zones\. In addition, you can roll back the updates if the new configuration isn't performing as you expected it to\. For more information, see [Using traffic flow to route DNS traffic](traffic-flow.md)\.

   For more information, see the following documentation:
   + [Choosing a routing policy](routing-policy.md)
   + [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)

1. Create health checks for the resources that you can't create alias records for, such as Amazon EC2 servers and email servers running in your data center\. You'll associate these health checks with your non\-alias records\.

   For more information, see [Creating, updating, and deleting health checks](health-checks-creating-deleting.md)\.

1. If necessary, configure router and firewall rules so that Route 53 can send regular requests to the endpoints that you specified in your health checks\. For more information, see [Configuring router and firewall rules for Amazon Route 53 health checksConfiguring router and firewall rules for health checks](dns-failover-router-firewall-rules.md)\.

1. Create all the non\-alias records in your diagram, and associate the health checks that you created in step 2 with the applicable records\.

   If you're configuring DNS failover in a configuration that doesn't include any alias records, skip the remaining tasks\.

1. Create the alias records that route traffic to AWS resources, such as ELB load balancers and CloudFront distributions\. If you want Route 53 to try another branch of the tree when a resource is unhealthy, set the value of **Evaluate Target Health** to **Yes** for each of your alias records\. \(**Evaluate Target Health** isn't supported for some AWS resources\.\)

1. Starting at the bottom of the tree diagram that you created in step 1, create the alias records that route traffic to the records that you created in steps 4 and 5\. If you want Route 53 to try another branch of the tree when all the non\-alias records are unhealthy in a branch of your tree, set the value of **Evaluate Target Health** to **Yes** for each of your alias records\.

   Remember that you can't create an alias record that routes traffic to another record until you have created the other record\. 