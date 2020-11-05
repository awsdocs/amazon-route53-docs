# Rule type<a name="resolver-rule-type"></a>

Choose the type of rule that you want to create:
+ **Forward**: Choose **Forward** when you want to forward DNS queries for specified domain names to DNS resolvers on your network\.
+ **System**: Choose **System** when you want to override the behavior that is defined in a forwarding rule\. When you create a system rule, Route 53 Resolver resolves DNS queries for specified subdomains that would otherwise be forwarded to \(and resolved by\) DNS resolvers in your network\.

## Learn more<a name="resolver-rule-type-learn-more"></a>
+ [Using rules to control which queries are forwarded to your network](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html#resolver-overview-forward-vpc-to-network-using-rules)
+ [Domain names that Resolver creates autodefined rules for](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html#resolver-overview-forward-vpc-to-network-autodefined-rules)