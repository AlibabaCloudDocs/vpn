# ModifyCustomerGatewayAttribute

Modifies the name and description of a customer gateway.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=ModifyCustomerGatewayAttribute&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyCustomerGatewayAttribute|The operation that you want to perform.

 Set the value to **ModifyCustomerGatewayAttribute**. |
|CustomerGatewayId|String|Yes|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the customer gateway. |
|RegionId|String|Yes|cn-shanghai|The ID of the region where the customer gateway is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|ClientToken|String|No|02fb3da4-130e-11e9-8e44-0016e04115b|The client token that is used to ensure the idempotence of the request.

 You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length.  |
|Description|String|No|test|The description of the customer gateway.

 The description must be 2 to 256 characters in length. It must start with a letter, and cannot start with `http://` or `https://`. |
|Name|String|No|test|The name of the customer gateway.

 The name must be 2 to 128 characters in length, and can contain, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter, and cannot start with `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CustomerGatewayId|String|cgw-bp1pvpl9r9adju6l5\*\*\*\*|The ID of the customer gateway. |
|Name|String|test|The name of the customer gateway. |
|Description|String|test|The description of the customer gateway. |
|IpAddress|String|139.196.32.xxx|The IP address of the customer gateway. |
|CreateTime|Long|1492747187000|The time when the customer gateway was created. |
|RequestId|String|E61293C8-AF07-4E87-A272-542680038F93|The ID of the request. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=ModifyCustomerGatewayAttribute
&CustomerGatewayId=vpn-bp1q8bgx4xnkm2ogj****
&RegionId=cn-shanghai
&Name=test
&<Common request parameters>

```

Sample success responses

`XML` format

```
<ModifyCustomerGatewayAttributeResponse>
      <CustomerGatewayId>cgw-bp1pvpl9r9adju6l5****</CustomerGatewayId>
      <RequestId>E61293C8-AF07-4E87-A272-542680038F93</RequestId>
      <CreateTime>1492747187000</CreateTime>
      <IpAddress>139.196.32.xxx</IpAddress>
</ModifyCustomerGatewayAttributeResponse>
```

`JSON` format

```
{
	"CustomerGatewayId":"cgw-bp1pvpl9r9adju6l5****",
	"CreateTime":1492747187000,
	"RequestId":"8AA5CE21-2E6A-4530-BDF5-F055849476E6",
	"IpAddress":"139.196.32.xxx"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. You can apply for the permission and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|404|InvalidCustomerGatewayInstanceId.NotFound|The specified customer gateway instance id does not exist.|The error message returned because the specified instance ID does not exist.|
|400|InvalidName|The name is not valid|The error message returned because the format of the specified name is invalid.|
|400|InvalidDescription|The description is not valid|The error message returned because the format of the specified description is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

