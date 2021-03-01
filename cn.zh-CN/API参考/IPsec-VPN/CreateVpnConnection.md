# CreateVpnConnection

调用CreateVpnConnection接口创建IPsec连接。

## 背景信息

普通型和国密型VPN网关在创建IPsec连接时支持的算法不同，在您创建IPsec连接前，建议您先了普通型和国密型VPN网关支持的算法信息。更多信息，请参见[创建VPN网关](~~65290~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=CreateVpnConnection&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateVpnConnection|要执行的操作，取值：**CreateVpnConnection**。 |
|CustomerGatewayId|String|是|cgw-bp1hgslrq1afztya\*\*\*\*|用户网关的ID。 |
|LocalSubnet|String|是|10.1.1.0/24,10.1.2.0/24|本端网段。

 需要和本地IDC互连的VPC侧的网段，用于第二阶段协商。

 多个网段之间用半角逗号（,）分隔，例如：192.168.1.0/24,192.168.2.0/24。 |
|RegionId|String|是|cn-shanghai|VPN网关所在地域ID。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|RemoteSubnet|String|是|10.2.1.0/24,10.2.2.0/24|对端网段。

 本地IDC的网段，用于第二阶段协商。

 多个网段之间用逗号（,）分隔，例如：192.168.3.0/24,192.168.4.0/24。 |
|VpnGatewayId|String|是|vpn-bp1q8bgx4xnkm\*\*\*\*|VPN网关的ID。 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-001\*\*\*\*|客户端Token，用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符。 |
|Name|String|否|IPsec|IPsec连接的名称。

 长度为2~128个字符，必须以英文字母或中文开头，可包含数字、半角句号（.）、下划线（\_）和短划线（-），但不能以`http://`或`https://`开头。 |
|EffectImmediately|Boolean|否|false|是否删除当前已协商成功的IPsec隧道并重新发起协商。取值：

 -   **true**：配置完成后立即进行协商。
-   **false**（默认值）：当有流量进入时进行协商。 |
|IkeConfig|String|否|\{"IkeVersion":"ikev1","IkeMode":"main","IkeEncAlg":"aes","IkeAuthAlg":"sha1","IkePfs":"group2","IkeLifetime":86400\}|第一阶段协商的配置信息：

 -   **Psk**：用于IPsec VPN网关与用户网关之间的身份认证。默认情况下会随机生成，也可以手动指定密钥。长度限制为100个字符。

**说明：** 仅在您为普通型VPN网关创建IPsec连接时需要配置该参数。

-   **IkeVersion**：IKE协议的版本。取值：**ikev1**或**ikev2**，默认值：**ikev1**。
-   **IkeMode**：IKE V1版本的协商模式。取值：**main**或**aggressive**，默认值：**main**。
-   **IkeEncAlg**：第一阶段协商的加密算法。
    -   为普通型VPN网关创建IPsec连接时，该参数取值：**aes**、**aes192**、**aes256**、**des**或**3des**，默认值：**aes**。
    -   为国密型VPN网关创建IPsec连接时，该参数默认值：**sm4**。
-   **IkeAuthAlg**：第一阶段协商的认证算法。
    -   为普通型VPN网关创建IPsec连接时，该参数取值：**md5**或**sha1**，默认值：**md5**。
    -   为国密型VPN网关创建IPsec连接时，该参数默认值：**sm3**。
-   **IkePfs**：第一阶段协商使用的Diffie-Hellman密钥交换算法。取值：**group1**、**group2**、**group5**或**group14**，默认值：**group2**。

**说明：** 仅在您为普通型VPN网关创建IPsec连接时需要配置该参数。

-   **IkeLifetime**：第一阶段协商出的SA的生存周期。取值范围为**0~86400**，单位为秒，默认值：**86400**。
-   **LocalIdIPsec**：VPN网关的标识。长度限制为100个字符，默认值为VPN网关的公网IP地址。

**说明：** 仅在您为普通型VPN网关创建IPsec连接时需要配置该参数。

-   **RemoteId**：
    -   在您为普通型VPN网关创建IPsec连接时，此参数为用户网关的标识。长度限制为100个字符，默认值为用户网关的公网IP地址。
    -   在您为国密型VPN网关创建IPsec连接时，此参数为对端CA证书的主体名称。例如："RemoteId":"CN=test,OU=test,O=test,C=CHN"。 |
|IpsecConfig|String|否|\{"IpsecEncAlg":"aes","IpsecAuthAlg":"sha1","IpsecPfs":"group2","IpsecLifetime":86400\}|第二阶段协商的配置信息：

 -   **IpsecEncAlg**：第二阶段协商的加密算法。
    -   为普通型VPN网关创建IPsec连接时，该参数取值：**aes**、**aes192**、**aes256**、**des**或**3des**，默认值：**aes**。
    -   为国密型VPN网关创建IPsec连接时，该参数默认值：**sm4**。
-   **IpsecAuthAlg**：第二阶段协商的认证算法。
    -   为普通型VPN网关创建IPsec连接时，该参数取值：**md5**或**sha1**，默认值：**md5**。
    -   为国密型VPN网关创建IPsec连接时，该参数默认值：**sm3**。
-   **IpsecPfs**：转发所有协议的报文。第二阶段协商使用的Diffie-Hellman密钥交换算法，取值：**group1**、**group2**、**group5**或**group14**，默认值：**group2**。

**说明：** 仅在您为普通型VPN网关创建IPsec连接时需要配置该参数。

-   **IpsecLifetime**：第二阶段协商出的SA的生存周期。取值范围为**0~86400**，单位为秒，默认值：**86400**。 |
|HealthCheckConfig|String|否|\{"enable":"true","dip":"192.XX.XX.2","sip":"192.XX.XX.2","interval":"3","retry":"3"\}|健康检查配置信息：

 -   **enable**：是否开启健康检查，取值：**true**或**false**，默认值：**false**。
-   **dip**：健康检查的目的IP地址。
-   **sip**：健康检查的源IP地址。
-   **interval**：健康检查的重试间隔时间。单位是秒。
-   **retry**：健康检查的重试发包次数。 |
|AutoConfigRoute|Boolean|否|true|是否自动配置路由，取值：

 -   **true**（默认值）：自动配置路由。
-   **false**：不自动配置路由。 |
|EnableDpd|Boolean|否|true|是否开启DPD（对等体存活检测）功能，取值：

 -   **true**（默认值）：开启DPD功能。IPsec发起端会发送DPD报文用来检测对端的设备是否存活，如果在设定时间内未收到正确回应则认为对端已经断线，IPsec将删除ISAKMP SA和相应的IPsec SA，安全隧道同样也会被删除。
-   **false**：不开启DPD功能，IPsec发起端不会发送DPD探测报文。 |
|EnableNatTraversal|Boolean|否|true|是否开启NAT穿越功能，取值：

 -   **true**（默认值）：开启NAT穿越功能。开启后，IKE协商过程会删除对UDP端口号的验证过程，同时实现对VPN隧道中NAT网关设备的发现功能。
-   **false**：不开启NAT穿越功能。 |
|BgpConfig|String|否|\{"EnableBgp":"true","LocalAsn":"45104","TunnelCidr":"169.254.11.0/30","LocalBgpIp":"169.254.11.1"\}|Bgp的配置信息：

 -   **EnableBgp**：是否开启Bgp功能，取值：**true**或**false**，默认值：**false**。
-   **LocalAsn**：本端自治系统号。
-   **TunnelCidr**：IPsec隧道网段，该网段应该是一个在169.254.0.0/16内掩码长度为30的网段。
-   **LocalBgpIp**：本端Bgp地址，该地址为IPsec隧道网段内的一个IP地址。 |
|RemoteCaCertificate|String|否|-----BEGIN CERTIFICATE----- MIIB7zCCAZW\*\*\*\*|为国密型VPN网关创建IPsec连接时，对端的CA证书。

 **说明：** 仅在您为国密型VPN网关创建IPsec连接时需要配置该参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|VpnConnectionId|String|vco-bp1dfksi8lnbvbegl\*\*\*\*|IPsec连接的ID。 |
|CreateTime|Long|1613806468000|IPsec连接的创建时间。 |
|Name|String|test|IPsec连接的名称。 |
|RequestId|String|CCBFF5D5-6388-4744-88D0-70CE4CC95F06|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateVpnConnection
&CustomerGatewayId=cgw-bp1hgslrq1afztya****
&LocalSubnet=10.1.1.0/24,10.1.2.0/24
&RegionId=cn-shanghai
&RemoteSubnet=10.2.1.0/24,10.2.2.0/24
&VpnGatewayId=vpn-bp1q8bgx4xnkm****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateVpnConnectionResponse>
  <RequestId>CCBFF5D5-6388-4744-88D0-70CE4CC95F06</RequestId>
  <CreateTime>1613806468000</CreateTime>
  <VpnConnectionId>vco-bp1dfksi8lnbvbegl****</VpnConnectionId>
</CreateVpnConnectionResponse>
```

`JSON`格式

```
{
  "RequestId": "CCBFF5D5-6388-4744-88D0-70CE4CC95F06",
  "CreateTime": 1613806468000,
  "VpnConnectionId": "vco-bp1dfksi8lnbvbegl****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|Resource.QuotaFull|The quota of resource is full|资源配额已达上限。|
|404|InvalidCustomerGatewayInstanceId.NotFound|The specified customer gateway instance id does not exist.|指定的 Instance 不存在，请您检查 Instance 是否正确。|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|指定的 VPN 网关不存在，请您检查 VPN 网关是否正确。|
|400|InvalidVpnConnection.AlreadyExists|Vpn connection already exists.|VPN 连接已经存在，不用再次添加。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|该服务已欠费，请您先充值再操作。|
|400|QuotaExceeded.PolicyBasedRoute|The maximum number of policy-based routes is exceeded. Existing routes: %s. Routes to be created: %s. Maximum routes: %s.|策略路由条数已达上限，当前已有%s条，本次将创建%s条，上限为%s条。|
|400|IllegalParam.LocalSubnet|The specified "LocalSubnet" \(%s\) is invalid.|本端网段\(%s\)不合法。|
|400|IllegalParam.RemoteSubnet|The specified "RemoteSubnet" \(%s\) is invalid.|对端网段\(%s\)不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

