# Making Amazon Route 53 the DNS service for an existing domain<a name="MigratingDNS"></a>

If you're transferring one or more domain registrations to Route 53, and you're currently using a domain registrar that doesn't provide paid DNS service, you need to migrate DNS service before you migrate the domain\. Otherwise, the registrar will stop providing DNS service when you transfer your domains, and the associated websites and web applications will become unavailable on the internet\. \(You can also migrate DNS service from the current registrar to another DNS service provider\. We don't require you to use Route 53 as the DNS service provider for domains that are registered with Route 53\.\)

The process depends on whether you're currently using the domain:
+ If the domain is currently getting traffic—for example, if your users are using the domain name to browse to a website or access a web application—see [Making Route 53 the DNS service for a domain that's in use](migrate-dns-domain-in-use.md)\.
+ If the domain isn't getting any traffic \(or is getting very little traffic\), see [Making Route 53 the DNS service for an inactive domain](migrate-dns-domain-inactive.md)\.

For both options, your domain should remain available during the entire migration process\. However, in the unlikely event that there are issues, the first option lets you roll back the migration quickly\. With the second option, your domain could be unavailable for a couple of days\.