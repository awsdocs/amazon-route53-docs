# Task List for Configuring DNS Failover<a name="dns-failover-how-to"></a>

To use Amazon Route 53 to configure DNS failover, perform the following tasks:

1. Draw a complete diagram of your configuration, and indicate which type of record you're creating \(weighted alias, failover, weighted, and so on\) for each node:

   + In a simple configuration, your diagram won't include any alias records\.

   + In a complex configuration, your diagram will include a combination of alias records \(such as weighted alias and failover alias\) and non\-alias records in a multi\-level tree like the examples in the topic [How Health Checks Work in Complex Amazon Route 53 Configurations](dns-failover-complex-configs.md)\.

1. Create health checks for each Amazon EC2 server and each non\-AWS resource, such as an email server running in your data center, that you want to include in your configuration\. You'll associate these health checks with your non\-alias records\.

   For more information, see [Creating, Updating, and Deleting Health Checks](health-checks-creating-deleting.md)\.

1. Create all of the non\-alias records in your diagram, and associate the health checks that you created in step 2 with the applicable records\.

   You can associate health checks with records by using the Amazon Route 53 console or the Amazon Route 53 API\. For more information, see the applicable documentation: 

   + **Using the Amazon Route 53 console:** See [Working with Resource Record Sets](rrsets-working-with.md)\.

   + **Using the Amazon Route 53 API:** See [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.
**Note**  
To quickly and easily create records for complex routing configurations and associate the records with health checks, you can use the traffic flow visual editor and save the configuration as a traffic policy\. You can then associate the traffic policy with one or more domain names \(such as example\.com\) or subdomain names \(such as www\.example\.com\), in the same hosted zone or in multiple hosted zones\. In addition, you can roll back the updates if the new configuration isn't performing as you expected it to\. For more information, see [Using Traffic Flow to Route DNS Traffic](traffic-flow.md)\.

   If you're configuring DNS failover in a simple configuration, with no alias records, skip the remaining tasks\.

1. Starting at the bottom of the tree diagram that you created in step 1, create the alias records \(such as weighted alias and failover alias records\) for which the alias target is one of the records that you created in step 3\. If you want Amazon Route 53 to try another branch of the tree when all of the non\-alias records are unhealthy in a branch of your tree, set the value of **Evaluate Target Health** to **Yes** for each of your alias records\.

1. If your tree diagram includes nodes for which you have not yet created alias records, create the remaining alias records, working from the bottom of the tree toward the top\.

   Remember that you cannot create an alias record if the alias target record doesn't exist yet\.