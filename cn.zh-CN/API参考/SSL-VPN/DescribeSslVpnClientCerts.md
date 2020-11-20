# DescribeSslVpnClientCerts

调用DescribeSslVpnClientCerts接口查询已创建的SSL客户端证书。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DescribeSslVpnClientCerts&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSslVpnClientCerts|要执行的操作，取值：**DescribeSslVpnClientCerts**。 |
|RegionId|String|是|cn-hangzhou|要查询的SSL客户端证书所在的地域。您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|Name|String|否|cert1|SSL客户端证书的名称。 |
|PageNumber|Integer|否|1|列表的页码，默认值为**1**。 |
|PageSize|Integer|否|10|分页查询时每页的行数，最大值为**50**，默认值为**10**。 |
|SslVpnClientCertId|String|否|vsc-bp1n8wcf134yl0osr\*\*\*\*|SSL客户端证书ID。 |
|SslVpnServerId|String|否|vss-bp18q7hzj6largv4v\*\*\*\*|SSL服务端ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|10|每页包含的条目数。 |
|RequestId|String|5BE01CD7-5A50-472D-AC14-CA181C5C03BE|请求ID。 |
|SslVpnClientCertKeys|Array| |SSL客户端证书的详细信息。 |
|SslVpnClientCertKey| | |SSL客户端证书的详细信息。 |
|CreateTime|Long|1492747187000|SSL客户端证书的创建时间。 |
|EndTime|Long|1494966335000|SSL客户端证书的到期时间。 |
|Name|String|cert1|SSL客户端证书的名称。 |
|RegionId|String|cn-hangzhou|SSL客户端证书的地域。 |
|SslVpnClientCertId|String|vsc-bp1n8wcf134yl0osr\*\*\*\*|SSL客户端证书的ID。 |
|SslVpnServerId|String|vss-bp18q7hzj6largv4v\*\*\*\*|SSL服务端ID。 |
|Status|String|normal|客户端证书的状态。

 -   **expiring-soon**：证书将在1周后过期。
-   **normal**：正常。
-   **expired**：已过期。 |
|TotalCount|Integer|1|列表条目数。 |

## 示例

请求示例

```

http(s)://vpc.aliyuncs.com/?Action=DescribeSslVpnClientCerts
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

```
{
	"DescribeSslVpnServersResponse":{
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
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

