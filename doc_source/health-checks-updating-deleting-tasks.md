# Updating or Deleting Health Checks when DNS Failover Is Configured<a name="health-checks-updating-deleting-tasks"></a>

When you want to update or delete health checks that are associated with records, or you want to change records that have associated health checks, you must consider how your changes affect routing of DNS queries and your DNS failover configuration\.

**Important**  
Amazon Route 53 does not prevent you from deleting a health check even if the health check is associated with one or more records\. If you delete a health check and you don't update the associated records, the future status of the health check cannot be predicted and might change\. This will affect the routing of DNS queries for your DNS failover configuration\. 

To update or delete health checks that are already associated with records, we recommend that you perform the following tasks:

1. Identify the records that are associated with the health checks\. To identify the records that are associated with a health check, you must do one of the following: 

   + Review the records in each hosted zone using the Amazon Route 53 console\. For more information, see [Listing Resource Record Sets](resource-record-sets-listing.md)\.

   + Run the `ListResourceRecordSets` API action on each hosted zone and review the response\. For more information, see [ListResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

1. Assess the change in behavior that will result from updating or deleting health checks, or from updating records, and determine which changes to make\. For more information, see the following topics:

   + [What Happens When You Omit Health Checks?](dns-failover-complex-configs.md#dns-failover-complex-configs-hc-omitting)

   + [Configuring Active\-Passive Failover by Using Amazon Route 53 Failover and Failover Alias Records](dns-failover-configuring-options.md#dns-failover-failover-rrsets)

1. Change health checks and records as applicable\. For more information, see the following topics:

   + [Creating and Updating Health Checks](health-checks-creating.md)

   + [Editing Resource Record Sets](resource-record-sets-editing.md)

1. Delete the health checks that you're no longer using, if any\. For more information about deleting health checks using the console, see [Deleting Health Checks](health-checks-deleting.md)\. For information about using the Amazon Route 53 API, see [DeleteHealthCheck](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHealthCheck.html) in the *Amazon Route 53 API Reference*\. 