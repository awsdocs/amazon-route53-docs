# Values that you specify when you register or transfer a domain<a name="domain-register-values-specify"></a>

When you register a domain or transfer domain registration to Amazon Route 53, you specify the values that are described in this topic\.

**Note**  
If you're registering more than one domain, Route 53 uses the values that you specify for all of the domains that are in your shopping cart\.

You can also change values for a domain that is currently registered with Route 53\. Note the following:
+ If you change contact information for the domain, we send an email notification to the registrant contact about the change\. This email comes from route53\-dev\-admin@amazon\.com\. For most changes, the registrant contact is not required to respond\.
+ For changes to contact information that also constitute a change in ownership, we send the registrant contact an additional email\. ICANN requires that the registrant contact confirm receiving the email\. For more information, see **First Name, Last Name** and **Organization** later in this section\.

For more information about changing settings for an existing domain, see [Updating settings for a domain](domain-update-settings.md)\.

**Values That You Specify**
+ [My Registrant, Administrative, and Technical contacts are all the same](#same-contacts-field)
+ [Contact Type](#contact-type-field)
+ [First Name, Last Name](#first-last-field)
+ [Organization](#organization-field)
+ [Email](#email-field)
+ [Phone](#phone-field)
+ [Address 1](#address-1-field)
+ [Address 2](#address-2-field)
+ [Country](#country-field)
+ [State](#state-field)
+ [City](#city-field)
+ [Postal/Zip Code](#postal-code-field)
+ [Fields for selected top-level domains](#tld-fields)
+ [Privacy Protection](#privacy-field)
+ [Auto Renew (Only available when editing domain settings)](#auto-renew-field)

**My Registrant, Administrative, and Technical contacts are all the same**  
Specifies whether you want to use the same contact information for the registrant of the domain, the administrative contact, and the technical contact\. 

**Contact Type**  
Category for this contact\. Note the following:  
+ If you choose an option other than **Person**, you must enter an organization name\.
+ For some TLDs, the privacy protection available depends on the value that you choose for **Contact Type**\. For the privacy protection settings for your TLD, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.
+ For \.es domains, the value of **Contact Type** must be **Person** for all three contacts\.

**First Name, Last Name**  
The first and last names of the contact\.  
For **First Name** and **Last Name**, we recommend that you specify the name on your official ID\. For some changes to domain settings, you must provide proof of identity, and the name on your ID must match the name of the registrant contact for the domain\.
If you're transferring a domain to Route 53 and the following are true, then you're changing the owner of the domain:  
+ The contact type is **Person**\.
+ You're changing the **First Name** and/or **Last Name** fields for the registrant contact from the current settings\. 
In that case, ICANN requires that we email the registrant contact to get approval\. The email comes from one of the following email addresses:    
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register-values-specify.html)
To determine who the registrar is for your TLD, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.  
The registrant contact must follow the instructions in the email to confirm that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\. 
If you change the email address of the registrant contact, this email is sent to the former email address and the new email address for the registrant contact\.  
Some TLD registrars charge a fee for changing the domain owner\. When you change one of these values, the Route 53 console displays a message that tells you whether there is a fee\.

**Organization**  
The organization that is associated with the contact, if any\. For the registrant and administrative contacts, this is typically the organization that is registering the domain\. For the technical contact, this might be the organization that manages the domain\.  
When the contact type is any value except **Person** and you change the **Organization** field for the registrant contact, you change the owner of the domain\. ICANN requires that we email the registrant contact to get approval\. The email comes from one of the following email addresses:    
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register-values-specify.html)
To determine who the registrar is for your TLD, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.  
If you change the email address of the registrant contact, this email is sent to the former email address and the new email address for the registrant contact\.  
Some TLD registrars charge a fee for changing the domain owner\. When you change the value of **Organization**, the Route 53 console displays a message that tells you whether there is a fee\.

**Email**  
The email address for the contact\.   
If you change the email address for the registrant contact, we send a notification email to the former email address and the new email address\. This email comes from route53\-dev\-admin@amazon\.com\. 

**Phone**  
The phone number for the contact:  
+ If you're entering a phone number for locations in the United States or Canada, enter **1** in the first field and the 10\-digit area code and phone number in the second field\.
+ If you're entering a phone number for any other location, enter the country code in the first field, and enter the rest of the phone number in the second field\. For a list of phone country codes, see the Wikipedia article [List of country calling codes](https://en.wikipedia.org/wiki/List_of_country_calling_codes)\.

**Address 1**  
The street address for the contact\.

**Address 2**  
Additional address information for the contact, for example, apartment number or mail stop\.

**Country**  
The country for the contact\.

**State**  
The state or province for the contact, if any\.

**City**  
The city for the contact\.

**Postal/Zip Code**  
The postal or zip code for the contact\.

**Fields for selected top\-level domains**  
The following top\-level domains \(TLDs\) require that you specify additional values:  
+ \.com\.au and \.net\.au
+ \.ca
+ \.es
+ \.fi
+ \.fr
+ \.it
+ \.ru
+ \.se
+ \.sg
+ \.co\.uk, \.me\.uk, and \.org\.uk
In addition, many TLDs require a VAT identification number\.  
For information about valid values, see [ExtraParam](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_ExtraParam.html) in the *Amazon Route 53 API Reference*\.

**Privacy Protection**  
Whether you want to conceal your contact information from WHOIS queries\. If you select **Hide contact information**, WHOIS \("who is"\) queries will return contact information for the registrar or the value "Protected by policy\."  
You must specify the same privacy setting for the administrative, registrant, and technical contacts\.
If you select **Don't hide contact information**, you'll get more email spam at the email address that you specified\.  
Anyone can send a WHOIS query for a domain and get back all of the contact information for that domain\. The WHOIS command is available in many operating systems, and it's also available as a web application on many websites\.   
Although there are legitimate users for the contact information associated with your domain, the most common users are spammers, who target domain contacts with unwanted email and bogus offers\. In general, we recommend that you choose **Hide contact information** for **Privacy Protection**\.
To enable or disable privacy protection for some domains, you must open a support case and request privacy protection\.  
For more information about privacy protection, see the following topics:  
+ [Enabling or disabling privacy protection for contact information for a domain](domain-privacy-protection.md)
+ [Domains that you can register with Amazon Route 53](registrar-tld-list.md)

**Auto Renew \(Only available when editing domain settings\)**  
Whether you want Route 53 to automatically renew the domain before it expires\. The registration fee is charged to your AWS account\. For more information, see [Renewing registration for a domain](domain-renew.md)\.  
If you disable automatic renewal, registration for the domain will not be renewed when the expiration date passes, and you might lose control of the domain name\. 
The period during which you can renew a domain name varies by top\-level domain \(TLD\)\. For an overview about renewing domains, see [Renewing registration for a domain](domain-renew.md)\. For information about extending domain registration for a specified number of years, see [Extending the registration period for a domain](domain-extend.md)\.