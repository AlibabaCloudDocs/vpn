# CreateVpnPbrRouteEntry

Creates a policy-based route for a VPN gateway.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=CreateVpnPbrRouteEntry&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateVpnPbrRouteEntry|The operation that you want to perform. Set the value to **CreateVpnPbrRouteEntry**. |
|NextHop|String|Yes|vco-bp15oes1py4i66rmd\*\*\*\*|The next hop of the policy-based route. |
|PublishVpc|Boolean|Yes|true|Specifies whether to advertise the policy-based route to the route table of the associated virtual private cloud \(VPC\). Valid values:

 -   **true**: Advertises the policy-based route to the route table of the associated VPC .
-   **false**: Does not advertise the policy-based route to the route table of the associated VPC. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the policy-based route is created. You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|RouteDest|String|Yes|10.0.0.0/24|The destination CIDR block of the policy-based route. |
|RouteSource|String|Yes|192.168.1.0/24|The source CIDR block of the policy-based route. |
|VpnGatewayId|String|Yes|vpn-bp1a3kqjiiq9legfx\*\*\*\*|The ID of the VPN gateway. |
|Weight|Integer|Yes|0|The weight of the policy-based route. Valid values: **0** and **100**. |
|ClientToken|String|No|d7d24a21-f4ba-4454-9173-b3828dae492b|The client token that is used to ensure the idempotence of the request.

 You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|Description|String|No|vpnroute1|The description of the policy-based route. |
|OverlayMode|String|No|Ipsec|The tunneling protocol. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CreateTime|Long|1492747187000|The time when the policy-based route was created. |
|Description|String|vpnroute1|The description of the policy-based route. |
|NextHop|String|vco-bp15oes1py4i66rmd\*\*\*\*|The next hop of the policy-based route. |
|OverlayMode|String|Ipsec|The tunneling protocol. |
|RequestId|String|5BE01CD7-5A50-472D-AC14-CA181C5C03BE|The ID of the request. |
|RouteDest|String|10.0.0.0/24|The destination CIDR block of the policy-based route. |
|RouteSource|String|192.168.1.0/24|The source CIDR block of the policy-based route. |
|State|String|normal|The status of the policy-based route. Valid values:

 -   **published**: The route is advertised.
-   **normal**: The route is not advertised. |
|VpnInstanceId|String|vpn-bp1cmw7jh1nfe43m9\*\*\*\*|The ID of the VPN gateway. |
|Weight|Integer|0|The weight of the policy-based route. Valid values: **0** and **100**. |

## Examples

Sample requests

```

http(s)://[Endpoint]/? Action=CreateVpnPbrRouteEntry
&NextHop=vco-bp15oes1py4i66rmd****
&PublishVpc=true
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
<CreateVpnPbrRouteEntryResponse>
	  <RouteDest>10.0.0.0/24</RouteDest>
	  <RouteSource>192.168.1.0/24</RouteSource>
	  <VpnInstanceId>vpn-bp1cmw7jh1nfe43m9****</VpnInstanceId>
	  <OverlayMode>Ipsec</OverlayMode>
	  <State>published</State>
	  <Weight>100</Weight>
	  <CreateTime>1563873294331</CreateTime>
	  <NextHop>vco-bp1tui07ob10fmuro****</NextHop>
</CreateVpnPbrRouteEntryResponse>
```

`JSON` format

```
{
	"RouteDest":"10.0.0.0/24",
	"VpnInstanceId":"vpn-bp1cmw7jh1nfe43m9****",
	"OverlayMode":"Ipsec",
	"Weight":100,
	"State":"published",
	"NextHop":"vco-bp1tui07ob10fmuro****",
	"CreateTime":1563873294331,
	"RouteSource":"192.168.1.0/24"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. You can apply for permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|400|Resource.QuotaFull|The quota of resource is full|The error message returned because the resource quota has reached the upper limit.|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|The error message returned because the specified VPN gateway does not exist. You can check whether the configuration of the VPN gateway is valid.|
|400|VpnGateway.Configuring|The specified service is configuring.|The error message returned because the specified service is being configured. Try again later.|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|The error message returned because the service is suspended due to overdue payments. Add funds before you enable the service.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

