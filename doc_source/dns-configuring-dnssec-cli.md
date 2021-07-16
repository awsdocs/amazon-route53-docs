# Using the AWS CLI to enable DNSSEC signing<a name="dns-configuring-dnssec-cli"></a>

You can use the AWS command line interface \(CLI\) to work with DNSSEC signing in Route 53\. For example, you can use the CLI to enable DNSSEC signing instead of enabling signing in the AWS Management Console\. This section provides an example of enabling DNSSEC signing by using the CLI\. For more information about using the CLI or SDKs to work with Route 53, see [Setting up Amazon Route 53](setting-up-route-53.md)\.

To use the Route 53 console to enable DNSSEC signing, see [Enabling DNSSEC signing and creating a KSK](dns-configuring-dnssec-enable-signing.md#dns-configuring-dnssec-enable)\.

Before you run the commands to enable DNSSEC signing, you must have a hosted zone in Route 53 and have access to the hosted zone ID\. You also must have access to a customer managed customer master key \(CMK\) in AWS Key Management Service \(AWS KMS\) that applies to DNSSEC\. 

Be aware that the customer managed CMK must be in the US East \(N\. Virginia\) Region\. In addition, Route 53 must have permission to access your customer managed CMK so that it can create a KSK for you\. To see the permissions that must be in place and to learn more about working with CMKs for DNSSEC, see [Working with customer managed CMKs for DNSSEC](dns-configuring-dnssec-cmk-requirements.md)\.\.

There are three steps to take to enable DNSSEC signing: 
+ Step 1: Create a key\-signing key \(KSK\)
+ Step 2: Enable signing
+ Step 3: Establish a chain of trust

This section includes example CLI commands for Step 1 and Step 2\. After you complete these steps, establish a chain of trust for the hosted zone to complete your DNSSEC signing setup\. For more information, see [Establishing a chain of trust](dns-configuring-dnssec-enable-signing.md#dns-configuring-dnssec-chain-of-trust)\.

Step 1: To create the KSK, run a command like the following, using your own values for `hostedzone_id`, `cmk_arn`, `ksk_name`, and `unique_string` \(to make the request unique\)\.

```
aws --region us-east-1 route53 create-key-signing-key \
			--hosted-zone-id $hostedzone_id \
			--key-management-service-arn $cmk_arn --name $ksk_name \
			--status ACTIVE \
			--caller-reference $unique_string
```

Step 2: To enable DNSSEC signing, run a command like the following, using your own value for the `hostedzone_id`:

```
aws --region us-east-1 route53 enable-hosted-zone-dnssec \
			--hosted-zone-id $hostedzone_id
```

Step 3: After you complete these steps, establish the chain of trust for the hosted zone\. For more information, see [Establishing a chain of trust](dns-configuring-dnssec-enable-signing.md#dns-configuring-dnssec-chain-of-trust)\.