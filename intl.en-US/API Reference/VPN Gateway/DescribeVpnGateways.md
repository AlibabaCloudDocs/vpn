# DescribeVpnGateways

Queries VPN gateways.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DescribeVpnGateways&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVpnGateways|The operation that you want to perform.

 Set the value to **DescribeVpnGateways**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the VPN gateway is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|BusinessStatus|String|No|Normal|The payment state of the VPN gateway.

 Valid values: **Normal and FinancialLocked**. |
|PageNumber|Integer|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: **50**. Default value: **10**. |
|Status|String|No|init|The status of the VPN gateway. Valid values:

 -   **init**
-   **provisioning**
-   **active**
-   **updating**
-   **deleting** |
|VpcId|String|No|vpc-bp1ub1yt9cvakoelj\*\*\*\*|The ID of the virtual private cloud \(VPC\) for which the VPN gateway is created. |
|VpnGatewayId|String|No|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the VPN gateway. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|VpnGateways| | |Detailed information about the VPN gateway. |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the VPN gateway. |
|VpcId|String|vpc-bp1ub1yt9cvakoelj\*\*\*\*|The ID of the VPC for which the VPN gateway is created. |
|VSwitchId|String|vsw-bp1y9ovl1cu9ou4tv\*\*\*\*|The ID of the VSwitch to which the VPN gateway belongs. |
|InternetIp|String|116.62.69.xxx|The public IP address of the VPN gateway. |
|CreateTime|Long|1515383700000|The time when the VPN gateway was created. |
|EndTime|Long|1518105600000|The time when the VPN gateway expires. |
|Spec|String|5M|The maximum bandwidth of the VPN gateway. |
|Name|String|test|The name of the VPN gateway. |
|Description|String|test|The description of the VPN gateway. |
|Status|String|active|The status of the VPN gateway. |
|BusinessStatus|String|Normal|The business state of the VPN gateway. |
|ChargeType|String|Prepay|The billing method of the VPN gateway. |
|IpsecVpn|String|enable|Indicates whether the IPsec-VPN feature is enabled. |
|SslMaxConnections|Long|5|The maximum number of concurrent SSL-VPN connections. |
|SslVpn|String|enable|Indicates whether the SSL-VPN feature is enabled. |
|Tag|String|1|The tag of the VPN gateway. |
|TotalCount|Integer|1|The number of entries returned. |
|PageNumber|Integer|1|The number of the returned page. |
|PageSize|Integer|10|The number of entries on the current page. |
|RequestId|String|DF11D6F6-E35A-41C3-9B20-6FC8A901FE65|The ID of the request. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=DescribeVpnGateways
&RegionId=cn-hangzhou
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DescribeVpnGatewaysResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <VpnGateways>
            <VpnGateway>
                  <Status>active</Status>
                  <VpnGatewayId>vpn-bp1q8bgx4xnkm2ogj****</VpnGatewayId>
                  <BusinessStatus>Normal</BusinessStatus>
                  <Spec>5M</Spec>
                  <CreateTime>1492753580000</CreateTime>
                  <InternetIp>116.62.69.xxx</InternetIp>
                  <EndTime>1495382400000</EndTime>
                  <VSwitchId>vsw-bp1y9ovl1cu9ou4tv****</VSwitchId>
                  <VpcId>vpc-bp1ub1yt9cvakoelj****</VpcId>
            </VpnGateway>
      </VpnGateways>
      <RequestId>DF11D6F6-E35A-41C3-9B20-6FC8A901FE65</RequestId>
</DescribeVpnGatewaysResponse>
```

`JSON` format

```
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"VpnGateways":{
		"VpnGateway":[
			{
				"Status":"active",
				"VpnGatewayId":"vpn-bp1q8bgx4xnkm2ogj****",
				"Spec":"5M",
				"BusinessStatus":"Normal",
				"CreateTime":1492753580000,
				"InternetIp":"116.62.69.xxx",
				"EndTime":1495382400000,
				"VSwitchId":"vsw-bp1y9ovl1cu9ou4tv****",
				"VpcId":"vpc-bp1ub1yt9cvakoelj****"
			}
		]
	},
	"RequestId":"B2CD1315-CA2B-47B1-9DA5-8F1D69C48E82"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. You can apply for the permission and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

