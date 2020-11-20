# DescribeSslVpnServers

Queries SSL-VPN servers.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DescribeSslVpnServers&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSslVpnServers|The operation that you want to perform.

 Set the value to **DescribeSslVpnServers**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the SSL-VPN server is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|Name|String|No|test|The name of the SSL-VPN server. |
|PageNumber|Integer|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: **50**. Default value: **10**. |
|SslVpnServerId|String|No|vss-bp15j3du13gq1dgey\*\*\*\*|The ID of the SSL-VPN server. |
|VpnGatewayId|String|No|vpn-bp1on0xae9d771ggi\*\*\*\*|The ID of the VPN gateway. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|085CA5EA-1E76-43A8-981B-E0208DECA0CB|The ID of the request. |
|SslVpnServers| | |Detailed information about the SSL-VPN server. |
|Cipher|String|AES-128-CBC|The encryption algorithm. |
|ClientIpPool|String|10.10.1.0/24|The client IP address pool. |
|Compress|Boolean|false|Indicates whether the transmitted data is compressed. |
|Connections|Integer|0|The total number of current connections. |
|CreateTime|Long|1544668844000|The time when the SSL-VPN server was created. |
|InternetIp|String|47.96.167.xxx|The public IP address. |
|LocalSubnet|String|192.168.0.0/24|The CIDR block of the client. |
|MaxConnections|Integer|5|The maximum number of connections. |
|Name|String|test|The name of the SSL-VPN server. |
|Port|Integer|1194|The port used by the SSL-VPN server. |
|Proto|String|UDP|The protocol used by the SSL-VPN server. |
|RegionId|String|cn-hangzhou|The ID of the region where the SSL-VPN server is created. |
|SslVpnServerId|String|vss-bp15j3du13gq1dgey\*\*\*\*|The ID of the SSL-VPN server. |
|VpnGatewayId|String|vpn-bp1on0xae9d771ggi\*\*\*\*|The ID of the VPN gateway. |
|TotalCount|Integer|1|The total number of entries returned. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=DescribeSslVpnServers
&RegionId=cn-hangzhou
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DescribeSslVpnServersResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <SslVpnServers>
            <SslVpnServer>
                  <RegionId>cn-hanghzou</RegionId>
                  <SslVpnServerId>vss-bp18q7hzj6largv4v****</SslVpnServerId>
                  <VpnGatewayId>vpn-bp1q8bgx4xnkm2ogj****</VpnGatewayId>
                  <Name>test</Name>
                  <CLientIpPool>10.10.10.20/24</CLientIpPool>
                  <LocalSubnet>10.10.10.10/24</LocalSubnet>
                  <Proto>UDP</Proto>
                  <Port>1194</Port>
                  <Cipher>AES-128-CBC</Cipher>
                  <Compress>true</Compress>
                  <CreateTime>1492753580000</CreateTime>
                  <Connections>0</Connections>
                  <MaxConnections>5</MaxConnections>
                  <InternetIp>47.98.xx.xx</InternetIp>
            </SslVpnServer>
      </SslVpnServers>
      <RequestId>DF11D6F6-E35A-41C3-9B20-6FC8A901FE65</RequestId>
</DescribeSslVpnServersResponse>
```

`JSON` format

```
{
	"PageNumber":"1",
	"TotalCount":"1",
	"SslVpnServers":{
		"SslVpnServer":{
			"VpnGatewayId":"vpn-bp1q8bgx4xnkm2ogj****",
			"CLientIpPool":"10.10.10.20/24",
			"Proto":"UDP",
			"Cipher":"AES-128-CBC",
			"InternetIp":"47.98.xx.xx",
			"SslVpnServerId":"vss-bp18q7hzj6largv4v****",
			"Name":"test",
			"Port":"1194",
			"MaxConnections":"5",
			"RegionId":"cn-hanghzou",
			"CreateTime":"1492753580000",
			"Compress":"true",
			"LocalSubnet":"10.10.10.10/24",
			"Connections":"0"
		}
	},
	"PageSize":"10",
	"RequestId":"DF11D6F6-E35A-41C3-9B20-6FC8A901FE65"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform this operation on the specified resource. You can apply for the permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform this operation on the specified resource. To acquire the required permissions, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

