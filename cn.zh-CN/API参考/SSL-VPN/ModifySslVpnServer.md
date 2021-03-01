# ModifySslVpnServer

调用ModifySslVpnServer接口修改SSL-VPN服务端的配置信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=ModifySslVpnServer&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifySslVpnServer|要执行的操作，取值：**ModifySslVpnServer**。 |
|RegionId|String|是|cn-hangzhou|VPN网关所在的地域ID。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|SslVpnServerId|String|是|vss-bp18q7hzj6largv4v\*\*\*\*|SSL-VPN服务端实例ID。 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-0016e04115b|客户端Token，用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大不超过64个ASCII字符。 |
|Name|String|否|test|SSL-VPN服务端的名称。

 长度为2~128个字符，必须以英文字母或中文开头，可包含数字、半角句号（.）、下划线（\_）和短划线（-），但不能以`http://` 或`https://`开头。 |
|ClientIpPool|String|否|10.30.30.0/24|客户端网段。 |
|LocalSubnet|String|否|10.20.20.0/24|本端网段。 |
|Proto|String|否|UDP|SSL-VPN服务端所使用的协议，取值：

 -   **TCP**：TCP协议。
-   **UDP**（默认值）：UDP协议。 |
|Cipher|String|否|AES-128-CBC|SSL-VPN使用的加密算法，取值：

 -   **AES-128-CBC**（默认值）：AES-128-CBC算法。
-   **AES-192-CBC**：AES-192-CBC算法。
-   **AES-256-CBC**：AES-256-CBC算法。
-   **none**：不使用加密算法。 |
|Port|Integer|否|1194|SSL-VPN服务端所使用的端口，默认值为**1194**。 不能用使用以下端口：

 **22**、**2222**、**22222**、**9000**、**9001**、**9002**、**7505**、**80**、**443**、**53**、**68**、**123**、**4510**、**4560**、**500**、**4500**。 |
|Compress|Boolean|否|false|指定是否对通信进行压缩， 取值：

 -   **true**：对通信进行压缩。
-   **false**（默认值）：对通信不进行压缩。 |
|EnableMultiFactorAuth|Boolean|否|true|是否开启双因子认证。取值：

 -   **true**：开启。
-   **false**（默认值）：不开启。

 **说明：** 如果您要使用双因子认证功能，请确保您的VPN网关是在2020年03月05日00时00分之后创建的，否则您的VPN网关将不支持双因子认证功能。 |
|IDaaSInstanceId|String|否|idaas-cn-hangzhou-p\*\*\*\*|IDaaS实例ID。 |
|IDaaSRegionId|String|否|cn-hangzhou|IDaaS实例所属地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Cipher|String|AES-128-CBC|使用的加密算法。 |
|ClientIpPool|String|10.30.30.0/24|客户端网段。 |
|Compress|Boolean|false|是否压缩通信。 |
|Connections|Integer|0|当前连接数。 |
|CreateTime|Long|1492753580000|创建SSL-VPN服务端的时间戳。 |
|EnableMultiFactorAuth|Boolean|true|是否开启了双因子认证。

 -   **true**：已开启。
-   **false**（默认值）：未开启。 |
|IDaaSInstanceId|String|idaas-cn-hangzhou-p\*\*\*\*|IDaaS实例ID。 |
|InternetIp|String|47.XX.XX.5|VPN网关的公网IP地址。 |
|LocalSubnet|String|10.20.20.0/24|本端网段。 |
|MaxConnections|Integer|5|最大连接数。 |
|Name|String|test|SSL-VPN服务端的名称。 |
|Port|Integer|1194|SSL-VPN服务端的端口。 |
|Proto|String|UDP|SSL-VPN服务端使用的协议。 |
|RegionId|String|cn-hangzhou|SSL-VPN服务端的地域ID。 |
|RequestId|String|E81C823E-9DC3-42AE-9358-5F0ECD55F856|请求ID。 |
|SslVpnServerId|String|vss-bp1phv0j000c78l3k\*\*\*\*|SSL-VPN服务端的ID。 |
|VpnGatewayId|String|vpn-bp17lofy9fd0dnvzv\*\*\*\*|VPN网关实例ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ModifySslVpnServer
&RegionId=cn-hangzhou
&SslVpnServerId=vss-bp18q7hzj6largv4v****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifySslVpnServerResponse>
  <LocalSubnet>10.20.20.0/24</LocalSubnet>
  <Compress>true</Compress>
  <Connections>0</Connections>
  <ClientIpPool>10.30.30.0/24</ClientIpPool>
  <RequestId>E81C823E-9DC3-42AE-9358-5F0ECD55F856</RequestId>
  <MaxConnections>5</MaxConnections>
  <EnableMultiFactorAuth>false</EnableMultiFactorAuth>
  <SslVpnServerId>vss-bp1phv0j000c78l3k****</SslVpnServerId>
  <CreateTime>1613800884000</CreateTime>
  <Port>1194</Port>
  <Name>test</Name>
  <Proto>UDP</Proto>
  <InternetIp>47.XX.XX.5</InternetIp>
  <VpnGatewayId>vpn-bp17lofy9fd0dnvzv****</VpnGatewayId>
  <RegionId>cn-hangzhou</RegionId>
  <Cipher>AES-128-CBC</Cipher>
</ModifySslVpnServerResponse>
```

`JSON`格式

```
{
  "LocalSubnet": "10.20.20.0/24",
  "Compress": true,
  "Connections": 0,
  "ClientIpPool": "10.30.30.0/24",
  "RequestId": "E81C823E-9DC3-42AE-9358-5F0ECD55F856",
  "MaxConnections": 5,
  "EnableMultiFactorAuth": false,
  "SslVpnServerId": "vss-bp1phv0j000c78l3k****",
  "CreateTime": 1613800884000,
  "Port": 1194,
  "Name": "test",
  "Proto": "UDP",
  "InternetIp": "47.XX.XX.5",
  "VpnGatewayId": "vpn-bp17lofy9fd0dnvzv****",
  "RegionId": "cn-hangzhou",
  "Cipher": "AES-128-CBC"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|InvalidName|The name is not valid|该名称格式不合法。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|该服务已欠费，请您先充值再操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

