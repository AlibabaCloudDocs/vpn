# DeleteVpnGateway

Deletes a VPN gateway.

**Note:** You cannot delete a VPN gateway that is associated with an IPsec-VPN connection.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DeleteVpnGateway&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteVpnGateway|The operation that you want to perform.

 Set the value to **DeleteVpnGateway**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the VPN gateway is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|VpnGatewayId|String|Yes|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the VPN gateway. |
|ClientToken|String|No|02fb3da4-130e-11e9-8e44-0016e04115b|The client token that is used to guarantee the idempotence of the request.

 You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|\>0ED8D006-F706-4D23-88ED-E11ED28DCAC0|The ID of the request. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=DeleteVpnGateway
&RegionId=cn-hangzhou
&VpnGatewayId=vpn-bp1q8bgx4xnkm2ogj****
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DeleteNatGatewayResponse>
      <RequestId>0ED8D006-F706-4D23-88ED-E11ED28DCAC0</RequestId>
</DeleteNatGatewayResponse>
```

`JSON` format

```
{
	"RequestId":"0ED8D006-F706-4D23-88ED-E11ED28DCAC0"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. You can apply for the permission and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|The error message returned because the specified VPN gateway does not exist. You can check whether the configuration of the VPN gateway is valid.|
|403|ForbiddenRelease|Forbidden to release a prepaid instance within validity period|The error message returned because you cannot release a subscription VPN gateway within the subscription duration.|
|400|VpnGateway.Configuring|The specified service is configuring.|The error message returned because the specified service is being configured. Try again later.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

