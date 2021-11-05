# High availability for Resolver endpoints<a name="best-practices-resolver-endpoint-high-availability"></a>

When you create your Route 53 Resolver inbound endpoints, Route 53 requires that you create at least two IP addresses that the DNS resolvers on your network will forward queries to\. You should also specify IP addressess in at least two Availability Zones for redundancy\. 

If you require more than one elastic network interface endpoint to be available at all times, we recommend that you create at least one more network interface than you need, to make sure you have additional capacity available for handling possible traffic surges\. The additional network interface also ensures availability during service operations like maintenance or upgrades\.

For more information, see [Values that you specify when you create or edit inbound endpoints](resolver-forwarding-inbound-queries.md#resolver-forwarding-inbound-queries-values)\.