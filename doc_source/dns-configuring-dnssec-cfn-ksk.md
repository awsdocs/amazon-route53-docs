# AWS::Route 53::KeySigningKey<a name="dns-configuring-dnssec-cfn-ksk"></a>

The `AWS::Route53::KeySigningKey` resource creates a new key\-signing key \(KSK\) in a hosted zone\. The hosted zone ID is passed as parameter in the KSK properties\. You can specify the properties of this KSK using the `Name`, `Status`, and `KeyManagementServiceArn` properties of the resource\.

## Syntax<a name="dns-configuring-dnssec-cfn-ksk.syntax"></a>

To declare this entity in your AWS CloudFormation template, use the following syntax:

**JSON**

```
{
  "Type" : "AWS::Route53::KeySigningKey",
  "Properties" : {
      "HostedZoneId" : String,
      "KeyManagementServiceArn" : String,
      "Name" : String,
      "Status" : String
    }
}
```

**YAML**

```
Type: AWS::Route53::KeySigningKey
Properties: 
  HostedZoneId: String
  KeyManagementServiceArn: String
  Name: String
  Status: String
```

## Properties<a name="dns-configuring-dnssec-cfn-ksk.properties"></a>

`HostedZoneId`  
A unique string \(ID\) that is used to identify a hosted zone\. For example: `Z00001111A1ABCaaABC11`\.   
*Required:* Yes  
*Type:* String  
*Update requires:* Replacement

`KeyManagementServiceArn`  
The Amazon resource name \(ARN\) for a customer managed customer master key \(CMK\) in AWS Key Management Service \(AWS KMS\. The `KeyManagementServiceArn` must be unique for each key\-signing key \(KSK\) in a single hosted zone\. For example: `arn:aws:kms:us-east-1:111122223333:key/111a2222-a11b-1ab1-2ab2-1ab21a2b3a111`\.   
*Required:* Yes  
*Type:* String  
*Update requires:* Replacement

`Name`  
A string used to identify a key\-signing key \(KSK\)\. `Name` can include numbers, letters, periods \(\.\), hyphens \(\-\), or underscores \(\_\)\. `Name` must be unique for each key\-signing key in the same hosted zone\.  
*Required:* Yes  
*Type:* String  
*Minimum:* 3  
*Maximum:* 128  
*Update requires:* Replacement

`Status`  
A string that represents the current key\-signing key \(KSK\) status\.  
Status can have one of the following values:    
SIGNING  
DNSSEC signing is enabled for the hosted zone\.  
NOT\_SIGNING  
DNSSEC signing is not enabled for the hosted zone\.  
DELETING  
DNSSEC signing is in the process of being removed for the hosted zone\.  
ACTION\_NEEDED  
There is a problem with signing in the hosted zone that requires you to take action to resolve\. For example, the customer managed customer master key \(CMK\) might have been deleted, or the permissions for the customer managed CMK might have been changed\.  
INTERNAL\_FAILURE  
There was an error during a request\. Before you can continue to work with DNSSEC signing, including with key\-signing keys \(KSKs\), you must correct the problem by enabling or disabling DNSSEC signing for the hosted zone\.

## Return values<a name="dns-configuring-dnssec-cfn-ksk.return-values"></a>

### Ref<a name="dns-configuring-dnssec-cfn-ksk.return-values.ref"></a>

When you pass the logical ID of this resource to the intrinsic `Ref` function, `Ref` returns the hosted zone ID\. For example: 

```
{ "Ref": "Z00001111A1ABCaaABC11" }
```

For more information about using the `Ref` function, see [ Ref](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\.