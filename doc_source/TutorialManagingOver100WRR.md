# Managing over 100 weighted records in Amazon Route 53<a name="TutorialManagingOver100WRR"></a>

Amazon Route 53 lets you configure weighted records\. For a given name and type \(for example, `www.example.com`, type A\), you can configure up to 100 alternative responses, each with its own weight\. When responding to queries for `www.example.com`, Route 53 DNS servers select a weighted random response to return to DNS resolvers\. The value of a weighted record that has a weight of 2 is returned, on average, twice as often as the value of a weighted record that has a weight of 1\.

If you need to direct traffic to more than 100 endpoints, one way to achieve this is to use a tree of weighted alias records and weighted records\. For example, the first "level" of the tree may be up to 100 weighted alias records, each of which can, in turn, point to up to 100 weighted records\. Route 53 permits up to three levels of recursion, allowing you to manage up to 1,000,000 unique weighted endpoints\.

A simple two\-level tree might look like this:

**Weighted alias records**
+ `www.example.com` aliases to `www-a.example.com` with a weight of 1
+ `www.example.com` aliases to `www-b.example.com` with a weight of 1

**Weighted records**
+ `www-a.example.com`, type A, value 192\.0\.2\.1, weight 1
+ `www-a.example.com`, type A, value 192\.0\.2\.2, weight 1
+ `www-b.example.com`, type A, value 192\.0\.2\.3, weight 1
+ `www-b.example.com`, type A, value 192\.0\.2\.4, weight 1

For more information about creating records, see [Working with records](rrsets-working-with.md)\.