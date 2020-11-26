# ListTagResources

Queries tags that are added to one or more resources.

## Description

-   Set **ResourceId.N** or **Tag.N that consists of Tag.N.Key and Tag.N.Value** in the request to specify the object to be queried.
-   **Tag.N** is the tag of a resource. Each tag consists of a key and a value. If you set only **Tag.N.Key**, all tag values that are associated with the specified key are returned. If you set only **Tag.N.Value**, an error message is returned.
-   If you set **Tag.N** and **ResourceId.N** to filter tags, **ResourceId.N** must match all specified key-value pairs.
-   If you specify multiple key-value pairs, resources that contain these key-value pairs are returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=ListTagResources&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ListTagResources|The operation that you want to perform. Set the value to **ListTagResources**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region to which the resource belongs. |
|ResourceType|String|Yes|VPC|The type of the resource. Valid values:

 -   **VPC**: a virtual private cloud \(VPC\)
-   **VSWITCH**: a VSwitch
-   **ROUTETABLE**: a route table
-   **EIP**: an elastic IP address \(EIP\)
-   **VpnGateway**: a VPN gateway
-   **NATGATEWAY**: a NAT gateway
-   **COMMONBANDWIDTHPACKAGE**: an EIP bandwidth plan |
|ResourceId.N|RepeatList|No|vpc-bp16qjewdsunr41m1\*\*\*\*|The ID of resource N. Valid values of N: **1** to **20**. |
|Tag.N.Key|String|No|FinanceDept|The key of the tag that is added to the resource. Valid values of N: **1** to **20**. The tag key cannot be an empty string. The key must be 1 to 64 characters in length, and start with a letter or Chinese character. It can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It cannot start with `aliyun` or `acs:`. It cannot contain `http://` or `https://`. |
|Tag.N.Value|String|No|FinanceJoshua|The value of tag N that is added to the resource. Valid values of N: **1** to **20**. The tag value can be an empty string. The tag value must be up to 128 characters in length, and start with a letter or Chinese character. It can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It cannot start with `aliyun` or `acs:`. It cannot contain `http://` or `https://`. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The query token. Set this parameter to the NextToken parameter value that is returned in the last API call. If no subsequent request is sent, you do not need to set this parameter. |
|MaxResults|Integer|No|50|The number of entries to return on each page. Valid values: **1** to **50**. Default value: **50**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token that is required for the next query. If the NextToken parameter is empty, no subsequent request will be sent. |
|RequestId|String|DE65F6B7-7566-4802-9007-96F2494AC512|The ID of the request. |
|TagResources|Array of TagResource| |The resources to which the tags are added. |
|TagResource| | | |
|ResourceId|String|vpc-bp16qjewdsunr41m1\*\*\*\*|The ID of the resource. |
|ResourceType|String|VPC|The type of the resource. Valid values:

 -   **VPC**: a VPC
-   **VSWITCH**: a VSwitch
-   **ROUTETABLE**: a route table
-   **EIP**: an EIP
-   **VpnGateway**: a VPN gateway
-   **NATGATEWAY**: a NAT gateway
-   **COMMONBANDWIDTHPACKAGE**: an EIP bandwidth plan |
|TagKey|String|FinanceDept|The key of the tag. |
|TagValue|String|FinanceJoshua|The value of the tag. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=VPC
&ResourceId.1=vpc-bp16qjewdsunr41m1****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ListTagResourcesResponse>
  <TagResources>
        <TagResource>
              <ResourceType>VPC</ResourceType>
              <TagValue>aa</TagValue>
              <TagKey>aaa</TagKey>
              <ResourcId>vpc-wz9aml8mptq6fsnfm****</ResourcId>
        </TagResource>
  </TagResources>
  <NextToken></NextToken>
  <RequestId>F11AC96F-B8E6-48F8-95CC-F63E7D50F0D4</RequestId>
</ListTagResourcesResponse>
```

`JSON` format

```
{
	"TagResources": {
		"TagResource": [
			{
				"ResourceType": "VPC",
				"TagValue": "aa",
				"TagKey": "aaa",
				"ResourcId": "vpc-wz9aml8mptq6fsnfm****"
			}
		]
	},
	"NextToken": "",
	"RequestId": "F11AC96F-B8E6-48F8-95CC-F63E7D50F0D4"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

