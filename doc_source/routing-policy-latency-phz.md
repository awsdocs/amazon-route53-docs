# Latency\-based routing in private hosted zones<a name="routing-policy-latency-phz"></a>

For private hosted zones, Route 53 answers DNS queries with an endpoint that is in the same AWS Region, or is closest in distance to the AWS Region of the VPC that the query originated from\.

If you include health checks, and the record with the lowest latency to the query's origin is unhealthy, a healthy endpoint with the next lowest latency is returned\.

In the example configuration in the following figure, DNS queries coming from an us\-east\-1 AWS Region, or closest to it, will be routed to the 1\.1\.1\.1 endpoint\. DNS queries from us\-west\-2, or closes to it, will be routed to the 2\.2\.2\.2 endpoint\.

![\[A screenshot that shows two latency records for a private hosted zone.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/latency-phz.png)