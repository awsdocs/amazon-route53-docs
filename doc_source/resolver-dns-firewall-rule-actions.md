# Rule actions in DNS Firewall<a name="resolver-dns-firewall-rule-actions"></a>

When DNS Firewall finds a match between a DNS query and a domain specification in a rule, it applies the action that's specified in the rule to the query\. 

You are required to specify one of the following options in each rule that you create: 
+ **Allow** – Stop inspecting the query and permit it to go through\. 
+ **Alert** – Stop inspecting the query, permit it to go through, and log an alert for the query in the Route 53 Resolver logs\. 
+ **Block** – Discontinue inspection of the query, block it from going to its intended destination, and log the block action for the query in the Route 53 Resolver logs\. 

  Reply with the configured block response, from the following: 
  + **NODATA** – Respond indicating that the query was successful, but no response is available for it\.
  + **NXDOMAIN**– Respond indicating that the query's domain name doesn't exist\.
  + **OVERRIDE**– Provide a custom override in the response\. This option requires the following additional settings: 
    + **Record value** – The custom DNS record to send back in response to the query\. 
    + **Record type**– The DNS record's type\. This determines the format of the record value\. This must be `CNAME`\.
    + **Time to live in seconds**– The recommended amount of time for the DNS resolver or web browser to cache the override record and use it in response to this query, if it is received again\. By default, this is zero, and the record isn't cached\.

For more information about the query logs configuration and the contents, see [Resolver query logging](resolver-query-logs.md) and [Values that appear in Resolver query logs](resolver-query-logs-format.md)\. 

**Use Alert to test blocking rules**  
When you first create a blocking rule, you can test it by configuring it with the action set to Alert\. You can then look at the number of queries that the rule alerts on to see how many would be blocked if you set the action to Block\. 