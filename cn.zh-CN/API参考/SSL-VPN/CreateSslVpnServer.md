# CreateSslVpnServer

调用CreateSslVpnServer接口创建SSL-VPN服务端。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=CreateSslVpnServer&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateSslVpnServer|要执行的操作，取值：**CreateSslVpnServer**。 |
|ClientIpPool|String|是|192.168.1.0/24|客户端网段。

 是给客户端虚拟网卡分配访问地址的的地址段，不是指客户端已有的内网网段。

 当客户端通过SSL-VPN连接访问本端时，VPN网关会从指定的客户端网段中分配一个IP地址给客户端使用。

 **说明：** 该网段不能与**LocalSubnet**地址段冲突。 |
|LocalSubnet|String|是|10.0.0.0/8|本端网段。

 是客户端通过SSL-VPN连接要访问的地址段。

 本端网段可以是VPC的网段、交换机的网段、通过专线和VPC互连的IDC的网段、云服务如对象存储服务OSS（Object Storage Service）等的网段。 |
|RegionId|String|是|cn-shanghai|VPN网关所在的地域ID。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpnGatewayId|String|是|vpn-bp1hgim8by0kc9nga\*\*\*\*|VPN网关的ID。 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-0016e04115b|客户端Token，用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大不值过64个ASCII字符。 |
|Name|String|否|sslvpnname|SSL-VPN服务端的名称。

 长度为2~128个字符，必须以英文字母或中文开头，可包含数字、半角句号（.）、下划线（\_）和短划线（-），但不能以`http://` 或`https://`开头。 |
|Proto|String|否|UDP|SSL-VPN服务端所使用的协议，取值：

 -   **TCP**：TCP协议。
-   **UDP**（默认值）：UDP协议。 |
|Cipher|String|否|AES-128-CBC|SSL-VPN使用的加密算法，取值：

 -   **AES-128-CBC**（默认值）：AES-128-CBC算法。
-   **AES-192-CBC**：AES-192-CBC算法。
-   **AES-256-CBC**：AES-256-CBC算法。
-   **none**：不使用加密算法。 |
|Port|Integer|否|1194|SSL-VPN服务端所使用的端口，默认值为**1194**。 不能用使用以下端口：

 **22、2222、22222、9000、9001、9002、7505、80、443、53、68、123、4510、4560、500、4500**。 |
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
|Name|String|test|SSL-VPN服务端的名称。 |
|RequestId|String|E98A9651-7098-40C7-8F85-C818D1EBBA85|请求ID。 |
|SslVpnServerId|String|vss-bp18q7hzj6largv4v\*\*\*\*|SSL-VPN服务端的ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateSslVpnServer
&ClientIpPool=192.168.1.0/24
&LocalSubnet=10.0.0.0/8
&RegionId=cn-shanghai
&VpnGatewayId=vpn-bp1hgim8by0kc9nga****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateSslVpnServerResponse>
      <RequestId>E98A9651-7098-40C7-8F85-C818D1EBBA85</RequestId>
      <SslVpnServerId>vss-bp18q7hzj6largv4v****</SslVpnServerId>
      <Name>test</Name>
</CreateSslVpnServerResponse>
```

`JSON`格式

```
{
    "RequestId": "E98A9651-7098-40C7-8F85-C818D1EBBA85",
    "SslVpnServerId": "vss-bp18q7hzj6largv4v****",
    "Name": "test"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|Resource.QuotaFull|The quota of resource is full|资源配额已达上限。|
|400|InvalidName|The name is not valid|该名称格式不合法。|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|指定的 VPN 网关不存在，请您检查 VPN 网关是否正确。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|该服务已欠费，请您先充值再操作。|
|400|QuotaExceeded.VpnRouteEntry|The number of route entries to the VPN gateway in the VPC routing table has reached the quota limit.|VPC路由表中指向VPN网关的路由条目已经达到配额限制。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

