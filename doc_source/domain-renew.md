# Renewing registration for a domain<a name="domain-renew"></a>

When you register a domain with Amazon Route 53 or you transfer domain registration to Route 53, we configure the domain to renew automatically\. The automatic renewal period is typically one year, although the registries for some top\-level domains \(TLDs\) have longer renewal periods\. For the registration and renewal period for your TLD, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.

**Note**  
You can't use AWS credits to pay the fee for renewing registration for a domain\.

For most top\-level domains \(TLDs\), you can change the expiration date for a domain\. For more information, see [Extending the registration period for a domain](domain-extend.md)\.

**Important**  
If you turn off automatic renewal, be aware of the following effects on your domain:  
Some TLD registries delete domains even before the expiration date if you don't renew early enough\. We strongly recommend that you leave automatic renewal enabled if you want to keep a domain name\.
We also strongly recommend that you don't plan to re\-register a domain after it has expired\. Some registrars allow others to register domains immediately after the domains expire, so you might not be able to re\-register before the domain is taken by someone else\.
Some registries charge a large premium to restore expired domains\.
On or near the expiration date, the domain becomes unavailable on the internet\.

To determine whether automatic renewal is enabled for your domain, see [Enabling or disabling automatic renewal for a domain](domain-enable-disable-auto-renewal.md)\.

If automatic renewal is enabled, here's what happens:

**45 days before expiration**  
We send an email to the registrant contact that tells you that automatic renewal is currently enabled and gives instructions about how to disable it\. Keep your registrant contact email address current so you don't miss this email\.

**35 or 30 days before expiration**  
For all domains except \.com\.ar, \.com\.br, and \.jp domains, we renew domain registration 35 days before the expiration date so we have time to resolve any issues with your renewal before the domain name expires\.  
The registries for \.com\.ar, \.com\.br, and \.jp domains require that we renew the domains no more than 30 days before expiration\. You'll get a renewal email from Gandi, our registrar associate, 30 days before expiration, which is the same day that we renew your domain if you have automatic renewal enabled\.  
When we renew your domain, we send you an email to let you know that we renewed it\. If the renewal failed, we send you an email to explain why it failed\.

If automatic renewal is disabled, here's what happens as the expiration date for a domain name approaches:

**45 days before expiration**  
We send an email to the registrant contact for the domain that tells you that automatic renewal is currently disabled and gives instructions about how to enable it\. Keep your registrant contact email address current so you don't miss this email\.

**30 days and 7 days before expiration**  
If automatic renewal is disabled for the domain, ICANN, the governing body for domain registration, requires the registrar to send you an email\. The email comes from one of the following email addresses:  
+ **noreply@registrar\.amazon\.com ** – For domains for which the registrar is Amazon Registrar\.
+ **noreply@domainnameverification\.net** – For domains for which the registrar is our registrar associate, Gandi\.
To determine who the registrar is for your TLD, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.  
If you enable automatic renewal less than 30 days before expiration, and the renewal period has not passed, we renew the domain within 24 hours\.  
Some TLD registries stop allowing renewals as much as 25 days before the expiration date, and many don't allow renewal after the expiration date\. In addition, processing a renewal can take up to a day\. If you delay too long before enabling automatic renewal, the domain might expire before renewal can be processed, and you might lose the domain\. If the expiration date is approaching, we recommend that you manually extend the expiration date for the domain\. For more information, see [Extending the registration period for a domain](domain-extend.md)\.
For more information about renewal periods, see the "Deadlines for renewing and restoring domains" section for your TLD in [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.

**After the expiration date**  
Most domains are held by the registrar for a brief time after expiration, so you might be able to renew an expired domain after the expiration date, but we strongly recommend that you keep automatic renewal enabled if you want to keep your domain\. For information about trying to renew a domain after the expiration date, see [Restoring an expired or deleted domain](domain-restore-expired.md)\.  
If your domain expires but late renewal is allowed for the domain, you can renew the domain for the standard renewal price\. To determine whether a domain is still within the late\-renewal period, perform the procedure in the [Extending the registration period for a domain](domain-extend.md) section\. If the domain is still listed, it's within the late\-renewal period\.  
For more information about renewal periods, see the "Deadlines for renewing and restoring domains" section for your TLD in [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.