# CreateVpnGateway

调用CreateVpnGateway接口创建VPN网关。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=CreateVpnGateway&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateVpnGateway|要执行的操作，取值：**CreateVpnGateway**。 |
|Bandwidth|Integer|是|5|VPN网关的公网带宽规格，单位Mbps。

 取值：**5**、**10**、**20**、**50**、**100**或**200**。 |
|RegionId|String|是|cn-hangzhou|VPN网关所在的地域。您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpcId|String|是|vpc-bp1ub1yt9cvakoelj\*\*\*\*|VPN网关所属的VPC实例ID。 |
|Name|String|否|MYVPN|VPN网关的名称，默认值为VPN网关的ID。

 长度为2~128个英文或中文字符，必须以大小写字母或中文开头，可包含数字、下划线（\_）和短划线（-），不能以`http://`或`https://`开头。 |
|InstanceChargeType|String|否|中国站示例值：PREPAY，国际站示例值：POSTPAY|VPN网关的计费方式。仅取值：**PREPAY**，包年包月。

 **说明：** 在您创建VPN网关时，该参数为必填项。 |
|Period|Integer|否|1|购买时长，取值：**1**~**9**、**12**、**24**、或**36**。单位：月。

 **说明：** **InstanceChargeType**参数的值为**PREPAY**时，该参数必选。 |
|AutoPay|Boolean|否|false|是否自动支付VPN网关的账单，取值：

 -   **true**：自动支付VPN网关的账单。
-   **false**（默认值）：不自动支付VPN网关的账单。 |
|EnableIpsec|Boolean|否|true|是否开启IPsec-VPN功能，取值：

 -   **true**（默认值）：开启IPsec-VPN功能。
-   **false**：不开启IPsec-VPN功能。 |
|EnableSsl|Boolean|否|true|是否开启SSL-VPN功能，取值：

 -   **true**：开启SSL-VPN功能。
-   **false**（默认值）：不开启SSL-VPN功能。 |
|SslConnections|Integer|否|5|允许同时连接的最大客户端数量，取值：**5**、**10**或**20**。 |
|VSwitchId|String|否|vsw-bp1j5miw2bae9s2vt\*\*\*\*|VPN网关所属的交换机的实例ID。 |
|VpnType|String|否|Normal|VPN网关类型。取值：

 -   **Normal**（默认值）：普通型。
-   **NationalStandard**：国密型。 |
|ClientToken|String|否|02fb3da4\*\*\*\*|客户端Token，用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Name|String|vpn-uf68lxhgr7ftbqr3p\*\*\*\*|VPN网关的名称。 |
|OrderId|Long|208240895400460|订单ID。

 如果您未选择自动支付VPN网关的账单，请前往阿里云控制台完成支付。 |
|RequestId|String|EB2C156A-41F8-49CC-A756-D55AFC8BFD69|请求ID。 |
|VpnGatewayId|String|vpn-uf68lxhgr7ftbqr3p\*\*\*\*|VPN网关实例ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateVpnGateway
&Bandwidth=5
&RegionId=cn-hangzhou
&VpcId=vpc-bp1ub1yt9cvakoelj****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateVpnGatewayResponse>
  <RequestId>EB2C156A-41F8-49CC-A756-D55AFC8BFD69</RequestId>
  <VpnGatewayId>vpn-uf68lxhgr7ftbqr3p****</VpnGatewayId>
  <OrderId>208240895400460</OrderId>
  <Name>vpn-uf68lxhgr7ftbqr3p****</Name>
</CreateVpnGatewayResponse>
```

`JSON`格式

```
{
  "RequestId": "EB2C156A-41F8-49CC-A756-D55AFC8BFD69",
  "VpnGatewayId": "vpn-uf68lxhgr7ftbqr3p****",
  "OrderId": 208240895400460,
  "Name": "vpn-uf68lxhgr7ftbqr3p****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Resource.QuotaFull|The quota of resource is full|资源配额已达上限。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

