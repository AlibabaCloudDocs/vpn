# UnTagResources

Removes tags from specified resources at a time.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=UnTagResources&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UnTagResources|The operation that you want to perform. Set the value to **UntagResources**. |
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
|TagKey.N|RepeatList|No|FinanceDept|The key of the tag you want to remove. Valid values of N: 1 to 20. It can be an empty string. The key must be up to 64 characters in length, and start with a letter or Chinese character. It can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It cannot start with `aliyun` or `acs:`. It cannot contain `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=UnTagResources
&RegionId=cn-hangzhou    
&ResourceId.1=vpc-bp16qjewdsunr41m1****
&ResourceType=VPC
&<Common request parameters>
```

Sample success responses

`XML` format

```
<UntagResourcesResponse>
      <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</UntagResourcesResponse>
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

