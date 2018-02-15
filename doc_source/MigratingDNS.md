# Migrating DNS Service for an Existing Domain to Amazon Route 53<a name="MigratingDNS"></a>

You can migrate DNS service for an existing domain to Route 53\. The process depends on whether you're currently using the domain:

+ If the domain is currently getting traffic—for example, if your users are using the domain name to browse to a website or access a web application—see [Migrating DNS Service for a Domain that's in Use](migrate-dns-domain-in-use.md)\.

+ If the domain isn't getting any traffic \(or is getting very little traffic\), see [Migrating DNS Service for an Inactive Domain](migrate-dns-domain-inactive.md)\.

For both options, your domain should remain available during the entire migration process\. However, in the unlikely event that there are issues, the first option lets you roll back the migration quickly\. With the second option, your domain could be unavailable for a couple of days\.