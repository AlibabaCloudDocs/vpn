# DescribeCustomerGateway

Queries a customer gateway.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DescribeCustomerGateway&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCustomerGateway|The operation that you want to perform.

 Set the value to **DescribeCustomerGateway**. |
|CustomerGatewayId|String|Yes|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the customer gateway. |
|RegionId|String|Yes|cn-shanghai|The ID of the region where the customer gateway is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CustomerGatewayId|String|cgw-bp1pvpl9r9adju6l5\*\*\*\*|The ID of the customer gateway. |
|Name|String|test|The name of the customer gateway. |
|Description|String|test|The description of the customer gateway. |
|IpAddress|String|139.196.32.xxx|The IP address of the customer gateway. |
|RequestId|String|99506ECB-218F-45A5-AE8E-79518451F615|The ID of the request. |
|CreateTime|Long|1492747187000|The time when the customer gateway was created. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=DescribeCustomerGateway
&CustomerGatewayId=vpn-bp1q8bgx4xnkm2ogj****
&RegionId=cn-shanghai
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DescribeCustomerGatewayResponse>
      <Name>test</Name>
      <CustomerGatewayId>cgw-bp1pvpl9r9adju6l5****</CustomerGatewayId>
      <CreateTime>1492747187000</CreateTime>
      <RequestId>99506ECB-218F-45A5-AE8E-79518451F615</RequestId>
      <IpAddress>139.196.32.xxx</IpAddress>
</DescribeCustomerGatewayResponse>
```

`JSON` format

```
{
	"Name":"test",
	"CustomerGatewayId":"cgw-bp1pvpl9r9adju6l5****",
	"CreateTime":1492747187000,
	"RequestId":"A0457BC9-6C0F-4437-AB9D-FB2EABC1D6A2",
	"IpAddress":"139.196.32.xxx"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. You can apply for the permission and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|404|InvalidCustomerGatewayInstanceId.NotFound|The specified customer gateway instance id does not exist.|The error message returned because the specified customer gateway does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

