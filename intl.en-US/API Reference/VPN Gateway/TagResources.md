# TagResources

Creates tags and adds the tags to specified resources at a time.

## Description

A tag is a label that you can add to an instance. Each tag consists of a key and a value. Before you add tags, take note of the following limits:

-   The keys of tags that are added to the same instance must be unique.
-   You cannot create tags without adding them to instances. All tags must be added to instances.
-   Tag information is not shared across regions.

    For example, in the China \(Shanghai\) region, you cannot view tags created in the China \(Hangzhou\) region.

-   Virtual private clouds \(VPCs\), route tables, VSwitches, and elastic IP addresses \(EIPs\) under the same account and in the same region share tag information with each other.

    For example, if you have added a tag to a VPC, the tag is available to VSwitches, route tables, and EIPs under the same account and in the same region where the VPC is created. You can select this tag from the editing page without the need to enter the tag again. You can modify the key and value of a tag or remove a tag from an instance anytime. After you delete an instance, all tags that are added to the instance are deleted.

-   You can add up to 20 tags to each instance. Before you add a tag to an instance, the system automatically checks the number of existing tags. If the maximum number of tags is reached, an error message is returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=TagResources&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|TagResources|The operation that you want to perform. Set the value to **TagResources**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region to which the resources belong. |
|ResourceId.N|RepeatList|Yes|vpc-bp16qjewdsunr41m1\*\*\*\*|The ID of resource N. Valid values of N: **1** to **20**. |
|ResourceType|String|Yes|VPC|The type of the resource. Valid values:

 -   **VPC**: a virtual private cloud \(VPC\)
-   **VSWITCH**: a VSwitch
-   **ROUTETABLE**: a route table
-   **EIP**: an elastic IP address \(EIP\)
-   **VpnGateway**: a VPN gateway
-   **NATGATEWAY**: a NAT gateway
-   **COMMONBANDWIDTHPACKAGE**: an EIP bandwidth plan |
|Tag.N.Key|String|No|FinanceDept|The key of tag N. Valid values of N: 1 to 20 It cannot be an empty string. The tag key must be 1 to 64 characters in length, and start with a letter or Chinese character. It can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\) and cannot start with `aliyun` or `acs:`. It cannot contain `http://` or `https://`. |
|Tag.N.Value|String|No|FinanceJoshua|The value of tag N. Valid values of N: 1 to 20. It can be an empty string. The tag value must be up to 128 characters in length, and start with a letter or Chinese character. It can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\) and cannot start with `aliyun` or `acs:`. It cannot contain `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|The ID of the request. |

## Examples

Sample requests

```
http(s)://vpc.aliyuncs.com/? Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=vpc-bp16qjewdsunr41m1****
&ResourceType=VPC
&Tag.1.Key=FinanceDept
&Tag.1.Value=FinanceJoshua
&<Common request parameters>
```

Sample success responses

`XML` format

```
<TagResourcesResponse>
      <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</TagResourcesResponse>
```

`JSON` format

```
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

