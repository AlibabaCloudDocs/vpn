# CreateIpsecServer

调用CreateIpsecServer创建IPsec服务端。

## 前提条件

创建IPsec服务端前，您需要先创建VPN网关并确保已开启VPN网关的SSL-VPN功能。具体操作，请参见[CreateVpnGateway](~~120363~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=CreateIpsecServer&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateIpsecServer|系统规定参数。取值：**CreateIpsecServer**。 |
|ClientIpPool|String|是|10.XX.XX.0/24|客户端网段，指给客户端虚拟网卡分配访问地址的地址段。

 **说明：** 客户端网段不能和VPC侧网段冲突。 |
|LocalSubnet|String|是|192.XX.XX.0/24|本端网段，指需要和客户端网段互连的VPC侧的网段。

 多个网段之间用半角逗号（,）分隔，例如：192.168.1.0/24,192.168.2.0/24。 |
|RegionId|String|是|cn-hangzhou|VPN网关所属地域ID。 |
|VpnGatewayId|String|是|vpn-bp17lofy9fd0dnvzv\*\*\*\*|VPN网关实例ID。 |
|IpSecServerName|String|否|test|IPsec服务端名称。

 名称长度为2~128个字符，以英文字母或中文开始，可包含数字、短划线（-）和下划线（\_）。 |
|EffectImmediately|Boolean|否|true|配置是否立即生效。取值：

 -   **true**：配置完成后立即进行协商。
-   **false**：当有流量进入时进行协商。 |
|IkeConfig|String|否|\{"IkeVersion":"ikev2","IkeMode":"main","IkeEncAlg":"aes","IkeAuthAlg":"sha1","IkePfs":"group2","IkeLifetime":86400\}|第一阶段协商参数配置。

 -   **IkeVersion**：IKE协议的版本。取值：**ikev1**或**ikev2**，默认值：**ikev2**。
-   **IkeMode**：IKE版本的协商模式。默认值：**main**。
-   **IkeEncAlg**：第一阶段协商的加密算法。默认值：**aes**。
-   **IkeAuthAlg**：第一阶段协商的认证算法。默认值：**sha1**。
-   **IkePfs**：第一阶段协商使用的Diffie-Hellman密钥交换算法。默认值：**group2**。
-   **IkeLifetime**：第一阶段协商出的SA的生存周期。默认值：**86400**，单位为秒。
-   **LocalId**：IPsec服务端标识。支持FQDN和IP地址格式，默认值为VPN网关公网IP地址。
-   **RemoteId**：对端标识。支持FQDN和IP地址格式，默认值为空。 |
|IpsecConfig|String|否|\{"IpsecEncAlg":"aes","IpsecAuthAlg":"sha1","IpsecPfs":"group2","IpsecLifetime":86400\}|第二阶段协商参数配置。

 -   **IpsecEncAlg**：第二阶段协商的加密算法。默认值：**aes**。
-   **IpsecAuthAlg**：第二阶段协商的认证算法。默认值：**sha1**。
-   **IpsecPfs**：转发所有协议的报文。第二阶段协商使用的Diffie-Hellman密钥交换算法。默认值：**group2**。
-   **IpsecLifetime**：第二阶段协商出的SA的生存周期。默认值：**86400**，单位为秒。 |
|PskEnabled|Boolean|否|true|是否开启预共享密钥认证方式。仅取值为**true**，表示开启预共享密钥认证方式。 |
|Psk|String|否|123456|预共享密钥。

 用于VPN网关与客户端之间的身份认证。默认情况下会随机生成一个16位的随机字符串，也可以手动指定密钥。长度限制为100个字符。 |
|ClientToken|String|否|d7d24a21-f4ba-4454-9173-b38\*\*\*\*|客户端Token，用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符。 |
|DryRun|String|否|false|是否只预检此次请求，取值：

 -   **true**：只预检此次请求，不会创建IPsec服务端。检查项包括是否填写了必需参数、请求格式、业务限制等。如果检查不通过，则返回对应错误信息。如果检查通过，则返回`DryRunOperation`。
-   **false**（默认值）：发送正常请求，通过检查后直接创建IPsec服务端。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|CreationTime|String|2021-02-22T03:24:28Z|IPsec服务端创建时间。

 T表示分隔符，Z表示的是UTC，即世界标准时间。 |
|IpsecServerId|String|iss-bp1jougp8cfsbo8y9\*\*\*\*|IPsec服务端ID。 |
|IpsecServerName|String|test|IPsec服务端名称。 |
|RegionId|String|cn-hangzhou|VPN网关所属地域ID。 |
|RequestId|String|690A967E-D4CD-4B69-8C78-94FE828BA10B|请求ID。 |
|VpnGatewayId|String|vpn-bp17lofy9fd0dnvzv\*\*\*\*|VPN网关实例ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateIpsecServer
&ClientIpPool=10.XX.XX.0/24
&LocalSubnet=192.XX.XX.0/24
&RegionId=cn-hangzhou
&VpnGatewayId=vpn-bp17lofy9fd0dnvzv****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateIpsecServerResponse>
  <RequestId>690A967E-D4CD-4B69-8C78-94FE828BA10B</RequestId>
  <VpnGatewayId>vpn-bp17lofy9fd0dnvzv****</VpnGatewayId>
  <IpsecServerId>iss-bp1jougp8cfsbo8y9****</IpsecServerId>
  <CreationTime>2021-02-22T03:24:28Z</CreationTime>
  <RegionId>cn-hangzhou</RegionId>
</CreateIpsecServerResponse>
```

`JSON`格式

```
{
"RequestId": "690A967E-D4CD-4B69-8C78-94FE828BA10B",
"VpnGatewayId": "vpn-bp17lofy9fd0dnvzv****",
"IpsecServerId": "iss-bp1jougp8cfsbo8y9****",
"CreationTime": "2021-02-22T03:24:28Z",
"RegionId": "cn-hangzhou"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|OperationUnsupported.IPsecServer|The current version of the VPN gateway does not support IPsec server.|当前VPN网关版本不支持IPsec服务端。|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|指定的 VPN 网关不存在，请您检查 VPN 网关是否正确。|
|400|VpnGateway.SslVpnDisabled|The VPN gateway has not enabled SSL VPN.|VPN网关没有开启SSL VPN功能。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|该服务已欠费，请您先充值再操作。|
|400|OperationFailed.IPsecServerExist|An IPsec server already exists in the VPN gateway.|VPN网关中已经存在一个IPsec服务端。|
|400|IllegalParam.LocalSubnet|The specified "LocalSubnet" \(%s\) is invalid.|本端网段\(%s\)不合法。|
|400|QuotaExceeded.VpnRouteEntry|The number of route entries to the VPN gateway in the VPC routing table has reached the quota limit.|VPC路由表中指向VPN网关的路由条目已经达到配额限制。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

