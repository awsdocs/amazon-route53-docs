# Configuring DNSSEC for a domain<a name="domain-configure-dnssec"></a>

Attackers sometimes hijack traffic to internet endpoints such as web servers by intercepting DNS queries and returning their own IP addresses to DNS resolvers in place of the actual IP addresses for those endpoints\. Users are then routed to the IP addresses provided by the attackers in the spoofed response, for example, to fake websites\. 

You can protect your domain from this type of attack, known as DNS spoofing or a man\-in\-the\-middle attack, by configuring Domain Name System Security Extensions \(DNSSEC\), a protocol for securing DNS traffic\. 

**Important**  
Amazon Route 53 supports DNSSEC for domain registration\. However, Route 53 does not support DNSSEC for DNS service, regardless of whether the domain is registered with Route 53\. If you want to configure DNSSEC for a domain that is registered with Route 53, you must either use another DNS service provider or set up your own DNS server\.

**Topics**
+ [Overview of how DNSSEC protects your domain](#domain-configure-dnssec-how-it-works)
+ [Prerequisites and maximums for configuring DNSSEC for a domain](#domain-configure-dnssec-prerequisites)
+ [Adding public keys for a domain](#domain-configure-dnssec-adding-keys)
+ [Deleting public keys for a domain](#domain-configure-dnssec-deleting-keys)

## Overview of how DNSSEC protects your domain<a name="domain-configure-dnssec-how-it-works"></a>

When you configure DNSSEC for your domain, a DNS resolver establishes a chain of trust for responses from intermediate resolvers\. The chain of trust begins with the TLD registry for the domain \(your domain's parent zone\) and ends with the authoritative name servers at your DNS service provider\. Not all DNS resolvers support DNSSEC; resolvers that don't support DNSSEC don't perform any signature or authenticity validation\.

Here's how you configure DNSSEC for domains registered with Amazon Route 53 to protect your internet hosts from DNS spoofing, simplified for clarity:

1. Use the method provided by your DNS service provider to *sign* the records in your hosted zone with the *private key* in an asymmetric key pair\.
**Important**  
Route 53 supports DNSSEC for domain registration but does not support DNSSEC for DNS service\. If you want to configure DNSSEC for a domain that is registered with Route 53, you must either use another DNS service provider or set up your own DNS server\.

1. Provide the *public key* from the key pair to your domain registrar, and specify the algorithm that was used to generate the key pair\. The domain registrar forwards the public key and the algorithm to the registry for the top\-level domain \(TLD\)\.

   For information about how to perform this step for domains that you registered with Route 53, see [Adding public keys for a domain](#domain-configure-dnssec-adding-keys)\.

After you configure DNSSEC, here's how it protects your domain from DNS spoofing:

1. Submit a DNS query, for example, by browsing to a website or by sending an email message\.

1. The request is routed to a DNS resolver\. Resolvers are responsible for returning the appropriate value to clients based on the request, for example, the IP address for the host that is running a web server or an email server\.

1. If the IP address is cached on the DNS resolver \(because someone else has already submitted the same DNS query, and the resolver already got the value\), the resolver returns the IP address to the client that submitted the request\. The client then uses the IP address to access the host\.

   If the IP address isn't cached on the DNS resolver, the resolver sends a request to the parent zone for your domain, at the TLD registry, which returns two values:
   + The Delegation Signer \(DS\) record, which is a public key that corresponds with the private key that was used to sign the record\.
   + The IP addresses of the authoritative name servers for your domain\.

1. The DNS resolver sends the original request to another DNS resolver\. If that resolver doesn't have the IP address, it repeats the process until a resolver sends the request to a name server at your DNS service provider\. The name server returns two values:
   + The record for the domain, such as example\.com\. Typically this contains the IP address of a host\.
   + The signature for the record, which you created when you configured DNSSEC\.

1. The DNS resolver uses the public key that you provided to the domain registrar \(and the registrar forwarded to the TLD registry\) to do to things:
   + Establish a chain of trust\.
   + Verify that the signed response from the DNS service provider is legitimate and hasn't been replaced with a bad response from an attacker\.

1. If the response is authentic, the resolver returns the value to the client that submitted the request\.

   If the response can't be verified, the resolver returns an error to the user\.

   If the TLD registry for the domain doesn't have the public key for the domain, the resolver responds to the DNS query by using the response that it got from the DNS service provider\. 

## Prerequisites and maximums for configuring DNSSEC for a domain<a name="domain-configure-dnssec-prerequisites"></a>

To configure DNSSEC for a domain, your domain and DNS service provider must meet the following prerequisites:
+ The registry for the TLD must support DNSSEC\. To determine whether the registry for your TLD supports DNSSEC, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.
+ The DNS service provider for the domain must support DNSSEC\.
**Important**  
Route 53 supports DNSSEC for domain registration but does not support DNSSEC for DNS service\. If you want to configure DNSSEC for a domain that is registered with Route 53, you must either use another DNS service provider or set up your own DNS server\.
+ You must configure DNSSEC with the DNS service provider for your domain before you add public keys for the domain to Route 53\.
+ The number of public keys that you can add to a domain depends on the TLD for the domain:
  + **\.com and \.net domains** – up to thirteen keys
  + **All other domains** – up to four keys

## Adding public keys for a domain<a name="domain-configure-dnssec-adding-keys"></a>

When you're rotating keys or you're enabling DNSSEC for a domain, perform the following procedure after you configure DNSSEC with the DNS service provider for the domain\.<a name="domain-configure-dnssec-adding-keys-procedure"></a>

**To add public keys for a domain**

1. If you haven't already configured DNSSEC with your DNS service provider, use the method provided by your service provider to configure DNSSEC\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered domains**\.

1. Choose the name of the domain that you want to add keys for\.

1. At the **DNSSEC status** field, choose **Manage keys**\.

1. Specify the following values:  
**Key type**  
Choose whether you want to upload a key\-signing key \(KSK\) or a zone\-signing key \(ZSK\)\.  
**Algorithm**  
Choose the algorithm that you used to sign the records for the hosted zone\.  
**Public key**  
Specify the public key from the asymmetric key pair that you used to configure DNSSEC with your DNS service provider\.   
Note the following:   
   + Specify the public key, not the digest\.
   + You must specify the key in base64 format\.

1. Choose **Add**\.
**Note**  
You can only add one public key at a time\. If you need to add more keys, wait until you receive a confirmation email from Route 53\.

1. When Route 53 receives a response from the registry, we send an email to the registrant contact for the domain\. The email either confirms that the public key has been added to the domain at the registry or explains why the key couldn't be added\.

## Deleting public keys for a domain<a name="domain-configure-dnssec-deleting-keys"></a>

When you're rotating keys or you're disabling DNSSEC for the domain, delete public keys using the following procedure before you disable DNSSEC with your DNS service provider\. We recommend that you wait for up to three days to delete public keys after you rotate keys or disable DNSSEC with your DNS service provider\. Note the following:
+ If you're rotating public keys, we recommend that you wait for up to three days after you add the new public keys to delete the old public keys\.
+ If you're disabling DNSSEC, delete public keys for the domain first\. We recommend that you wait for up to three days before you disable DNSSEC with the DNS service for the domain\. 

**Important**  
If DNSSEC is enabled for the domain and you disable DNSSEC with the DNS service, DNS resolvers that support DNSSEC will return a `SERVFAIL` error to clients, and the clients won't be able to access the endpoints that are associated with the domain\. <a name="domain-configure-dnssec-deleting-keys-procedure"></a>

**To delete public keys for a domain**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered domains**\.

1. Choose the name of the domain that you want to delete keys from\.

1. At the **DNSSEC status** field, choose **Manage keys**\.

1. Find the key that you want to delete, and choose **Delete**\.
**Note**  
You can only delete one public key at a time\. If you need to delete more keys, wait until you receive a confirmation email from Amazon Route 53\.

1. When Route 53 receives a response from the registry, we send an email to the registrant contact for the domain\. The email either confirms that the public key has been deleted from the domain at the registry or explains why the key couldn't be deleted\.