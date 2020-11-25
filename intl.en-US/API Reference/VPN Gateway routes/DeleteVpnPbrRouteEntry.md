# DeleteVpnPbrRouteEntry

Deletes a VPN policy-based route.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DeleteVpnPbrRouteEntry&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteVpnPbrRouteEntry|The operation that you want to perform. Set the value to **DeleteVpnPbrRouteEntry**. |
|NextHop|String|Yes|vco-bp15oes1py4i66rmd\*\*\*\*|The next hop of the policy-based route. |
|RegionId|String|Yes|cn-hangzhou|The region of the VPN policy-based route. You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|RouteDest|String|Yes|10.0.0.0/24|The destination CIDR block of the policy-based route. |
|RouteSource|String|Yes|192.168.1.0/24|The source CIDR block of the policy-based route. |
|VpnGatewayId|String|Yes|vpn-bp1a3kqjiiq9legfx\*\*\*\*|The ID of the VPN gateway. |
|Weight|Integer|Yes|0|The weight of the policy-based route. Valid values: **0** or **100**. |
|ClientToken|String|No|d7d24a21-f4ba-4454-9173-b3828dae492b|The client token that is used to ensure the idempotence of the request.

 The client generates the value. Ensure that the value is unique among different requests. The token must contain 1 to 64 ASCII characters in length. |
|OverlayMode|String|No|Ipsec|The tunneling protocol. Set the value to **Ipsec** \(IPsec tunneling protocol\). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5BE01CD7-5A50-472D-AC14-CA181C5C03BE|The ID of the request. |

## Examples

Sample requests

```

http(s)://[Endpoint]/? Action=DeleteVpnPbrRouteEntry
&NextHop=vco-bp15oes1py4i66rmd****
&RegionId=cn-hangzhou
&RouteDest=10.0.0.0/24
&RouteSource=192.168.1.0/24
&VpnGatewayId=vpn-bp1a3kqjiiq9legfx****
&Weight=0
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DeleteVpnPbrRouteEntryResponse>
      <RequestId>5BE01CD7-5A50-472D-AC14-CA181C5C03BE</RequestId>
</DeleteVpnPbrRouteEntryResponse>
```

`JSON` format

```
{
	"RequestId":"E82612A9-CB90-4D7E-B394-1DB7F6509B29"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are not authorized to perform this operation on the specified resource. You can apply for the permission and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are not authorized to perform this operation on the specified resource. To acquire the required permissions, submit a ticket.|
|400|Resource.QuotaFull|The quota of resource is full|The error message returned because the resource quota has reached the upper limit.|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|The error message returned because the specified VPN gateway does not exist. You can check whether the configuration of the VPN gateway is valid.|
|400|VpnGateway.Configuring|The specified service is configuring.|The error message returned because the specified service is being configured. Try again later.|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|The error message returned because the service is overdue. Add funds before you enable the service.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

