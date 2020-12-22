# AWS::Route 53::DNSSEC<a name="dns-configuring-dnssec-cfn-dnssec"></a>

The `AWS::Route53::DNSSEC` resource is used to enable DNSSEC in a hosted zone\.

## Syntax<a name="dns-configuring-dnssec-cfn-dnssec.syntax"></a>

To declare this entity in your AWS CloudFormation template, use the following syntax:

**JSON**

```
{
  "Type" : "AWS::Route53::DNSSEC",
  "Properties" : {
      "HostedZoneId" : String
    }
}
```

**YAML**

```
Type: AWS::Route53::DNSSEC
Properties: 
  HostedZoneId: String
```

## Properties<a name="dns-configuring-dnssec-cfn-dnssec.properties"></a>

`HostedZoneId`  
A unique string \(ID\) that is used to identify a hosted zone\. For example: `Z00001111A1ABCaaABC11`\.   
*Required:* Yes  
*Type:* String  
*Update requires:* Replacement

## Return values<a name="dns-configuring-dnssec-cfn-dnssec.return-values"></a>

### Ref<a name="dns-configuring-dnssec-cfn-dnssec.return-values.ref"></a>

When you pass the logical ID of this resource to the intrinsic `Ref` function, `Ref` returns the hosted zone ID\. For example: 

```
{ "Ref": "Z00001111A1ABCaaABC11" }
```

For more information about using the `Ref` function, see [ Ref](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html) in the *AWS CloudFormation User Guide*\.