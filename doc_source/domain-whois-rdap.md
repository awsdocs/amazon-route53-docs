# Viewing information about domains that are registered with Amazon Registrar<a name="domain-whois-rdap"></a>

You can view information about \.com, \.net, and \.org domains that were registered using Route 53 and for which Amazon Registrar is the registrar\. This information includes details such as when the domain was originally registered and contact information for the domain owner and for the technical and administrative contacts\.

Note the following:

**Emailing domain contacts when privacy protection is enabled**  
If privacy protection is enabled for the domain, contact information for the registrant, technical, and administrative contacts is replaced with contact information for the Amazon Registrar privacy service\. For example, if the example\.com domain is registered with Amazon Registrar and if privacy protection is enabled, the value of **Registrant Email** in the response to a WHOIS query would be similar to owner1234@example\.com\.whoisprivacyservice\.org\.  
To contact one or more domain contacts when privacy protection is enabled, send an email to the corresponding email addresses\. We automatically forward your email to the applicable contact\. 

**Reporting abuse**  
To report any illegal activity or violation of the [Acceptable Use Policy](http://aws.amazon.com/route53/amazon-registrar-policies/#acceptable-use-policy), including inappropriate content, phishing, malware, or spam, send an email to abuse@amazon\.com\.<a name="domain-whois-rdap-procedure"></a>

**To view information about domains that are registered with Amazon Registrar**

1. In a web browser, go to one of the following websites\. Both websites display the same information, they just use different protocols and display the information in different formats:
   + **WHOIS:** [https://registrar\.amazon\.com/whois](https://registrar.amazon.com/whois)
   + **RDAP:** [https://registrar\.amazon\.com/rdap](https://registrar.amazon.com/rdap)

1. Enter the name of the domain that you want to view information about, and choose **Search**\.