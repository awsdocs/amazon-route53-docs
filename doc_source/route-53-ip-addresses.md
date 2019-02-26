# IP Address Ranges of Amazon Route 53 Servers<a name="route-53-ip-addresses"></a>

Amazon Web Services \(AWS\) publishes its current IP address ranges in JSON format\. To view the current ranges, download [ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. For more information, see [AWS IP Address Ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the *Amazon Web Services General Reference*\.

To find the IP address ranges that are associated with Amazon Route 53 name servers, search ip\-ranges\.json for the following string:

`"service": "ROUTE53"`

To find the IP address ranges that are associated with Route 53 health checkers, search ip\-ranges\.json for the following string:

`"service": "ROUTE53_HEALTHCHECKS"`