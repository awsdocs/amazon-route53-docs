# Resolver query log example<a name="resolver-query-logs-example-json"></a>

Here's an example query log:

```
	    {
	        "version": "1.000000",
	        "account_id": "111122223333",
	        "region": "us-west-2",
	        "vpc_id": "vpc-7example",
	        "query_timestamp": "2020-07-27T16:32:20Z",
	        "query_name": "api.example.com.",
	        "query_type": "A",
	        "query_class": "IN",
	        "rcode": "NOERROR",
	        "answers": [
	            {
	                "Rdata": "192.0.2e.44",
	                "Type": "A",
	                "Class": "IN"
	            },
	            {
	                "Rdata": "198.51.100.6",
	                "Type": "A",
	                "Class": "IN"
	            },
	            {
	                "Rdata": "203.0.113.8",
	                "Type": "A",
	                "Class": "IN"
	            },
	            {
	                "Rdata": "203.0.113.9",
	                "Type": "A",
	                "Class": "IN"
	            }
	        ],
	        "srcaddr": "192.0.2.15",
	        "srcport": "50637",
	        "transport": "UDP",
	        "srcids": {
	            "instance": "i-0d15cd0d3example"
	            "resolver-endpoint": "rslvr-out-2345678dfghexample"
	        }
```