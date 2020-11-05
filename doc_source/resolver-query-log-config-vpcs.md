# VPCs that queries are logged for<a name="resolver-query-log-config-vpcs"></a>

A query logging configuration sends query logs to the destination that you specified for queries that originate in the VPCs that you choose in the **VPCs that queries are logged for** section\. The table in this section displays the following values for each VPC:
+ **VPC ID**: The ID of a VPC that this query logging configuration is logging DNS queries for\. 
+ **VPC name**: The name of the VPC that this query logging configuration is logging DNS queries for\. 
+ **Logging status**: The logging status is one of the following values:
  + `ACTIVE`: Resolver associated the Amazon VPC with the query logging configuration, and is now logging queries that originate in the VPC\.
  + `CREATING`: Resolver is associating the Amazon VPC with the query logging configuration\.
  + `CREATED`: Resolver successfully associated the Amazon VPC with the query logging configuration\. Resolver is logging queries that originate in the specified VPC\.
  + `DELETING`: Resolver is deleting the association between the VPC and the configuration\.
  + `FAILED`: Resolver either couldn't create or couldn't delete an association between the VPC and the configuration\.
+ **Query logging configs**: The number of query logging configurations that are logging DNS queries that originate in the VPC\.
+ **Owner**: The account number of the AWS account that created the VPC\.

## Learn more<a name="resolver-query-log-config-vpcs-learn-more"></a>
+ [Resolver query Logging](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html)
+ [Configuring Resolver query logging](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html#resolver-query-logs-configuring)
+ [AWS resources that you can send Resolver query logs to](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html#resolver-query-logs-choosing-target-resource)