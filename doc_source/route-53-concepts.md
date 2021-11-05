# Amazon Route 53 concepts<a name="route-53-concepts"></a>

Here's an overview of the concepts that are discussed throughout the *Amazon Route 53 Developer Guide*\.

**Topics**
+ [Domain registration concepts](#route-53-concepts-domain-registration)
+ [Domain Name System \(DNS\) concepts](#route-53-concepts-domain-name-system-dns)
+ [Health checking concepts](#route-53-concepts-health-checking)

## Domain registration concepts<a name="route-53-concepts-domain-registration"></a>

Here's an overview of the concepts that are related to domain registration\.
+ [domain name](#route-53-concepts-domain-name)
+ [domain registrar](#route-53-concepts-domain-registrar)
+ [domain registry](#route-53-concepts-domain-registry)
+ [domain reseller](#route-53-concepts-domain-reseller)
+ [top-level domain (TLD)](#route-53-concepts-top-level-domain)

**domain name**  
The name, such as example\.com, that a user types in the address bar of a web browser to access a website or a web application\. To make your website or web application available on the internet, you start by registering a domain name\. For more information, see [How domain registration works](welcome-domain-registration.md)\.

**domain registrar**  
A company that is accredited by ICANN \(Internet Corporation for Assigned Names and Numbers\) to process domain registrations for specific top\-level domains \(TLDs\)\. For example, Amazon Registrar, Inc\. is a domain registrar for \.com, \.net, and \.org domains\. Our registrar associate, Gandi, is a domain registrar for hundreds of TLDs, such as \.apartments, \.boutique, and \.camera\. For more information, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.

**domain registry**  
A company that owns the right to sell domains that have a specific top\-level domain\. For example, [VeriSign](http://www.verisign.com/) is the registry that owns the right to sell domains that have a \.com TLD\. A domain registry defines the rules for registering a domain, such as residency requirements for a geographic TLD\. A domain registry also maintains the authoritative database for all of the domain names that have the same TLD\. The registry's database contains information such as contact information and the name servers for each domain\. 

**domain reseller**  
A company that sells domain names for registrars such as Amazon Registrar\. Amazon Route 53 is a domain reseller for Amazon Registrar and for our registrar associate, Gandi\.

**top\-level domain \(TLD\)**  
The last part of a domain name, such as \.com, \.org, or \.ninja\. There are two types of top\-level domains:     
**Generic top\-level domains**  
These TLDs typically give users an idea of what they'll find on the website\. For example, domain names that have a TLD of *\.bike* often are associated with websites for motorcycle or bicycle businesses or organizations\. With a few exceptions, you can use any generic TLD you want, so a bicycle club could use the \.hockey TLD for their domain name\.  
**Geographic top\-level domains**  
These TLDs are associated with geographic areas such as countries or cities\. Some registries for geographic TLDs have residency requirements, while others, such as [\.io \(British Indian Ocean Territory\)](io.md), allow or even encourage use as a generic TLD\. 
For a list of the TLDs that you can use when you register a domain name with Route 53, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.

## Domain Name System \(DNS\) concepts<a name="route-53-concepts-domain-name-system-dns"></a>

Here's an overview of the concepts that are related to the Domain Name System \(DNS\)\.
+ [alias record](#route-53-concepts-alias-resource-record-set)
+ [authoritative name server](#route-53-concepts-authoritative-name-server)
+ [DNS query](#route-53-concepts-dns-query)
+ [DNS resolver](#route-53-concepts-dns-resolver)
+ [Domain Name System (DNS)](#route-53-concepts-domain-name-system)
+ [hosted zone](#route-53-concepts-hosted-zone)
+ [IP address](#route-53-concepts-ip-address)
+ [name servers](#route-53-concepts-name-servers)
+ [private DNS](#route-53-concepts-private-dns)
+ [recursive name server](#route-53-concepts-recursive-name-server)
+ [record (DNS record)](#route-53-concepts-resource-record-set)
+ [reusable delegation set](#route-53-concepts-reusable-delegation-set)
+ [routing policy](#route-53-concepts-routing-policy)
+ [subdomain](#route-53-concepts-subdomain)
+ [time to live (TTL)](#route-53-concepts-time-to-live)

**alias record**  
A type of record that you can create with Amazon Route 53 to route traffic to AWS resources such as Amazon CloudFront distributions and Amazon S3 buckets\. For more information, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**authoritative name server**  
A name server that has definitive information about one part of the Domain Name System \(DNS\) and that responds to requests from a DNS resolver by returning the applicable information\. For example, an authoritative name server for the \.com top\-level domain \(TLD\) knows the names of the name servers for every registered \.com domain\. When a \.com authoritative name server receives a request from a DNS resolver for example\.com, it responds with the names of the name servers for the DNS service for the example\.com domain\.  
Route 53 name servers are the authoritative name servers for every domain that uses Route 53 as the DNS service\. The name servers know how you want to route traffic for your domain and subdomains based on the records that you created in the hosted zone for the domain\. \(Route 53 name servers store the hosted zones for the domains that use Route 53 as the DNS service\.\)  
For example, if a Route 53 name server receives a request for www\.example\.com, it finds that record and returns the IP address, such as 192\.0\.2\.33, that is specified in the record\.

**DNS query**  
Usually a request that is submitted by a device, such as a computer or a smart phone, to the Domain Name System \(DNS\) for a resource that is associated with a domain name\. The most common example of a DNS query is when a user opens a browser and types the domain name in the address bar\. The response to a DNS query typically is the IP address that is associated with a resource such as a web server\. The device that initiated the request uses the IP address to communicate with the resource\. For example, a browser can use the IP address to get a web page from a web server\. 

**DNS resolver**  
A DNS server, often managed by an internet service provider \(ISP\), that acts as an intermediary between user requests and DNS name servers\. When you open a browser and enter a domain name in the address bar, your query goes first to a DNS resolver\. The resolver communicates with DNS name servers to get the IP address for the corresponding resource, such as a web server\. A DNS resolver is also known as a recursive name server because it sends requests to a sequence of authoritative DNS name servers until it gets the response \(typically an IP address\) that it returns to a user's device, for example, a web browser on a laptop computer\.

**Domain Name System \(DNS\)**  
A worldwide network of servers that help computers, smart phones, tablets, and other IP\-enabled devices to communicate with one another\. The Domain Name System translates easily understood names such as example\.com into the numbers, known as *IP addresses*, that allow computers to find each other on the internet\.  
See also [IP address](#route-53-concepts-ip-address)\.

**hosted zone**  
A container for records, which include information about how you want to route traffic for a domain \(such as example\.com\) and all of its subdomains \(such as www\.example\.com, retail\.example\.com, and seattle\.accounting\.example\.com\)\. A hosted zone has the same name as the corresponding domain\.   
For example, the hosted zone for example\.com might include a record that has information about routing traffic for www\.example\.com to a web server that has the IP address 192\.0\.2\.243, and a record that has information about routing email for example\.com to two email servers, mail1\.example\.com and mail2\.example\.com\. Each email server also requires its own record\.  
See also [record (DNS record)](#route-53-concepts-resource-record-set)\.

**IP address**  
A number that is assigned to a device on the internet—such as a laptop, a smart phone, or a web server—that allows the device to communicate with other devices on the internet\. IP addresses are in one of the following formats:  
+ Internet Protocol version 4 \(IPv4\) format, such as 192\.0\.2\.44
+ Internet Protocol version 6 \(IPv6\) format, such as 2001:0db8:85a3:0000:0000:abcd:0001:2345
Route 53 supports both IPv4 and IPv6 addresses for the following purposes:  
+ You can create records that have a type of A, for IPv4 addresses, or a type of AAAA, for IPv6 addresses\.
+ You can create health checks that send requests either to IPv4 or to IPv6 addresses\.
+ If a DNS resolver is on an IPv6 network, it can use either IPv4 or IPv6 to submit requests to Route 53\.

**name servers**  
Servers in the Domain Name System \(DNS\) that help to translate domain names into the IP addresses that computers use to communicate with one another\. Name servers are either recursive name servers \(also known as [DNS resolver](#route-53-concepts-dns-resolver)\) or [authoritative name server](#route-53-concepts-authoritative-name-server)s\.  
For an overview of how DNS routes traffic to your resources, including the role of Route 53 in the process, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\.

**private DNS**  
A local version of the Domain Name System \(DNS\) that lets you route traffic for a domain and its subdomains to Amazon EC2 instances within one or more Amazon virtual private clouds \(VPCs\)\. For more information, see [Working with private hosted zones](hosted-zones-private.md)\.

**record \(DNS record\)**  
An object in a hosted zone that you use to define how you want to route traffic for the domain or a subdomain\. For example, you might create records for example\.com and www\.example\.com that route traffic to a web server that has an IP address of 192\.0\.2\.234\.  
For more information about records, including information about functionality that is provided by Route 53–specific records, see [Configuring Amazon Route 53 as your DNS service](dns-configuring.md)\.

**recursive name server**  
See [DNS resolver](#route-53-concepts-dns-resolver)\.

**reusable delegation set**  
A set of four authoritative name servers that you can use with more than one hosted zone\. By default, Route 53 assigns a random selection of name servers to each new hosted zone\. To make it easier to migrate DNS service to Route 53 for a large number of domains, you can create a reusable delegation set and then associate the reusable delegation set with new hosted zones\. \(You can't change the name servers that are associated with an existing hosted zone\.\)  
You create a reusable delegation set and associate it with a hosted zone programmatically; using the Route 53 console isn't supported\. For more information, see [CreateHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html) and [CreateReusableDelegationSet](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateReusableDelegationSet.html) in the *Amazon Route 53 API Reference*\. The same feature is also available in the [AWS SDKs](https://docs.aws.amazon.com/), the [AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/reference/route53/index.html), and [AWS Tools for Windows PowerShell](https://docs.aws.amazon.com/powershell/latest/reference/)\.

**routing policy**  
A setting for records that determines how Route 53 responds to DNS queries\. Route 53 supports the following routing policies:  
+ **Simple routing policy** – Use to route internet traffic to a single resource that performs a given function for your domain, for example, a web server that serves content for the example\.com website\.
+ **Failover routing policy** – Use when you want to configure active\-passive failover\. 
+ **Geolocation routing policy** – Use when you want to route internet traffic to your resources based on the location of your users\.
+ **Geoproximity routing policy** – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another\.
+ **Latency routing policy** – Use when you have resources in multiple locations and you want to route traffic to the resource that provides the best latency\.
+ **Multivalue answer routing policy** – Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random\.
+ **Weighted routing policy** – Use to route traffic to multiple resources in proportions that you specify\.
For more information, see [Choosing a routing policy](routing-policy.md)\.

**subdomain**  
A domain name that has one or more labels prepended to the registered domain name\. For example, if you register the domain name example\.com, then www\.example\.com is a subdomain\. If you create the hosted zone accounting\.example\.com for the example\.com domain, then seattle\.accounting\.example\.com is a subdomain\.  
To route traffic for a subdomain, create a record that has the name that you want, such as www\.example\.com, and specify the applicable values, such as the IP address of a web server\. 

**time to live \(TTL\)**  
The amount of time, in seconds, that you want a DNS resolver to cache \(store\) the values for a record before submitting another request to Route 53 to get the current values for that record\. If the DNS resolver receives another request for the same domain before the TTL expires, the resolver returns the cached value\.  
A longer TTL reduces your Route 53 charges, which are based in part on the number of DNS queries that Route 53 responds to\. A shorter TTL reduces the amount of time that DNS resolvers route traffic to older resources after you change the values in a record, for example, by changing the IP address for the web server for www\.example\.com\.

## Health checking concepts<a name="route-53-concepts-health-checking"></a>

Here's an overview of the concepts that are related to Amazon Route 53 health checking\.
+ [DNS failover](#route-53-concepts-dns-failover)
+ [endpoint](#route-53-concepts-endpoint)
+ [health check](#route-53-concepts-health-check)

**DNS failover**  
A method for routing traffic away from unhealthy resources and to healthy resources\. When you have more than one resource performing the same function—for example, more than one web server or mail server—you can configure Route 53 health checks to check the health of your resources and configure records in your hosted zone to route traffic only to healthy resources\.   
For more information, see [Configuring DNS failover](dns-failover-configuring.md)\.

**endpoint**  
The resource, such as a web server or an email server, that you configure a health check to monitor the health of\. You can specify an endpoint by IPv4 address \(192\.0\.2\.243\), by IPv6 address \(2001:0db8:85a3:0000:0000:abcd:0001:2345\), or by domain name \(example\.com\)\.   
You can also create health checks that monitor the status of other health checks or that monitor the alarm state of a CloudWatch alarm\. 

**health check**  
A Route 53 component that lets you do the following:  
+ Monitor whether a specified endpoint, such as a web server, is healthy
+ Optionally, get notified when an endpoint becomes unhealthy
+ Optionally, configure DNS failover, which allows you to reroute internet traffic from an unhealthy resource to a healthy resource
For more information about how to create and use health checks, see [Creating Amazon Route 53 health checks and configuring DNS failover](dns-failover.md)\.