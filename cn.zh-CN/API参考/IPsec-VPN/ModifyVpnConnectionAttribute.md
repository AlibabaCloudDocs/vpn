# ModifyVpnConnectionAttribute

调用ModifyVpnConnectionAttribute接口修改IPsec连接的配置信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=ModifyVpnConnectionAttribute&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyVpnConnectionAttribute|要执行的操作，取值：**ModifyVpnConnectionAttribute**。 |
|RegionId|String|是|cn-shanghai|IPsec连接所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpnConnectionId|String|是|vco-bp1bbi27hojx80nck\*\*\*\*|IPsec连接的ID。 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-0016e04115b|用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符。 |
|Name|String|否|IPsec|IPsec连接的名称。

 长度为2~128个字符，必须以字母或中文开头，可包含数字、点号（.）、下划线（\_）和短横线（-）。但不能以`http://`或`https://`开头。 |
|LocalSubnet|String|否|1.1.1.0/24,1.1.2.0/24|需要和本地IDC互连的VPC侧的网段，用于第二阶段协商。

 多个网段之间用逗号（,）分隔，例如：192.168.1.0/24,192.168.2.0/24。 |
|RemoteSubnet|String|否|1.1.1.0/24,1.1.2.0/24|本地IDC的网段，用于第二阶段协商。

 多个网段之间用逗号（,）分隔，例如：192.168.3.0/24,192.168.4.0/24。 |
|EffectImmediately|Boolean|否|false|是否删除当前已协商成功的IPsec隧道并重新发起协商。取值：

 -   **true**：配置完成后立即进行协商。
-   **false**（默认值）：当有流量进入时进行协商。 |
|IkeConfig|String|否|\{"IkeVersion":"ikev1","IkeMode":"main","IkeEncAlg":"aes","IkeAuthAlg":"sha1","IkePfs":"group2","IkeLifetime":86400\}|第一阶段协商的配置信息：

 -   **IkeConfig.Psk**：用于IPsec VPN网关与用户网关之间的身份认证。默认情况下会随机生成，也可以手动指定密钥。长度限制为100个字符。
-   **IkeConfig.IkeVersion**：IKE协议的版本。取值：ikev1\|ikev2，默认值：ikev1。
-   **IkeConfig.IkeMode**：IKE V1版本的协商模式。取值：main（主模式）\|aggressive（野蛮模式），默认值：main。
-   **IkeConfig.IkeEncAlg**：第一阶段协商的加密算法，取值：aes\|aes192\|aes256\|des\|3des，默认值：aes。
-   **IkeConfig.IkeAuthAlg**：第一阶段协商的认证算法，取值：md5\|sha1，默认值：sha。

IkeConfig.IkePfs：第一阶段协商使用的Diffie-Hellman密钥交换算法，取值：group1\|group2\|group5\|group14\|group24，默认值：group2。

-   **IkeConfig.IkeLifetime**：第一阶段协商出的SA的生存周期。取值范围为0~86400，单位为秒，默认值：86400。
-   **IkeConfig.LocalIdIPsec**：VPN网关的标识，长度限制为100个字符，默认值为VPN网关的公网IP地址。
-   **IkeConfig.RemoteId**：用户网关的标识，长度限制为100个字符，默认值为用户网关的公网IP地址。 |
|IpsecConfig|String|否|\{"IpsecEncAlg":"aes","IpsecAuthAlg":"sha1","IpsecPfs":"group2","IpsecLifetime":86400\}|第二阶段协商的配置信息：

 -   **IpsecConfig.IpsecEncAlg**：第二阶段协商的加密算法，取值：aes\|aes192\|aes256\|des\|3des，默认值：aes。
-   **IpsecConfig. IpsecAuthAlg**：第二阶段协商的认证算法，取值：md5\|sha1，默认值：sha1。
-   **IpsecConfig. IpsecPfs**：转发所有协议的报文。第一阶段协商使用的Diffie-Hellman密钥交换算法，取值：group1\|group2\|group5\|group14\|group24，默认值：group2。
-   **IpsecConfig. IpsecLifetime**：第二阶段协商出的SA的生存周期。取值范围为0~86400，单位为秒，默认值：86400。 |
|HealthCheckConfig|String|否|\{"enable":"true","dip":"192.168.xx.2","sip":"192.168.xx.2","interval":"3","retry":"3"\}|健康检查配置信息：

 -   **HealthCheckConfig.enable**：是否开启健康检查，取值：**true\|false**（默认值）。
-   **HealthCheckConfig.dip**：健康检查的目的IP地址。
-   **HealthCheckConfig.sip**：健康检查的源IP地址。
-   **HealthCheckConfig.interval**：健康检查的重试间隔时间，单位是秒。
-   **HealthCheckConfig.retry**：健康检查的重试发包次数。 |
|AutoConfigRoute|Boolean|否|true|是否自动发布路由，取值：

 -   **true**（默认值）：自动发布。
-   **false**：不自动发布。 |
|EnableDpd|Boolean|否|true|是否开启DPD（对等体存活检测）功能，取值：

 -   **true**（默认值）：开启DPD功能。IPsec发起端会发送DPD报文用来检测对端的设备是否存活，如果在设定时间内未收到正确回应则认为对端已经断线，IPsec将删除ISAKMP SA和相应的IPsec SA，安全隧道同样也会被删除。
-   **false**：不开启DPD功能，IPsec发起端不会发送DPD探测报文。 |
|EnableNatTraversal|Boolean|否|true|是否开启NAT穿越功能，取值：

 -   **true**（默认值）：开启NAT穿越功能。开启后，IKE协商过程会删除对UDP端口号的验证过程，同时实现对VPN隧道中NAT网关设备的发现功能。
-   **false**：不开启NAT穿越功能。 |
|BgpConfig|String|否|\{"EnableBgp":"true","LocalAsn":"10001","TunnelCidr":"169.254.11.0/30","LocalBgpIp":"169.254.11.1"\}|Bgp的配置信息：

 -   **BgpConfig.EnableBgp**：是否开启Bgp功能，取值：**true** \| **false**。
-   **BgpConfig.LocalAsn**：本端自治系统号。
-   **BgpConfig.TunnelCidr**：IPsec隧道网段，该网段在169.254.0.0/16内的掩码长度为30的网段。
-   **LocalBgpIp**：本端Bgp地址，该地址为IPsec隧道网段内的一个IP地址。 |
|RemoteCaCertificate|String|否|c20ycDI1NnYxIENBIChURVNUIFN\*\*\*\*|国密型VPN网关创建IPsec连接时，对端的CA证书。

 -   对于国密型VPN网关，创建IPsec连接时，此项必填。
-   对于普通型VPN网关，此项需要为空。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|VpnConnectionId|String|vco-bp1bbi27hojx80nck\*\*\*\*|IPsec连接的ID。 |
|CustomerGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|用户网关的ID。 |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关的ID。 |
|Name|String|test|IPsec连接的名称。 |
|LocalSubnet|String|1.1.1.0/24,1.1.2.0/24|VPC侧的网段。 |
|RemoteSubnet|String|1.1.1.0/24,1.1.2.0/24|本地IDC侧的网段。 |
|CreateTime|Long|1492753817000|IPsec连接的创建时间。 |
|Description|String|description|IPsec描述信息。 |
|EffectImmediately|Boolean|false|IPsec连接是否立即生效。

 -   **true**：配置完成后立即进行协商。
-   **false**（默认值）：当有流量进入时进行协商。 |
|EnableDpd|Boolean|true|是否开启DPD（对等体存活检测）功能。

 -   **false**：未开启。
-   **true**：已开启。 |
|EnableNatTraversal|Boolean|true|是否开启NAT穿越功能。

 -   **false**：未开启。
-   **true**：已开启。 |
|IkeConfig|Struct| |第一阶段协商的配置。 |
|IkeAuthAlg|String|sha1|IKE认证算法。 |
|IkeEncAlg|String|aes|IKE加密算法。 |
|IkeLifetime|Long|86400|IKE生存时间。 |
|IkeMode|String|main|IKE模式。 |
|IkePfs|String|group2|DH分组。 |
|IkeVersion|String|ikev1|IKE版本。 |
|LocalId|String|116.xx.xx.64|本端ID，支持FQDN和IP格式，默认为当前选取的VPN网关IP地址。 |
|Psk|String|pgw6dy7d1i8i\*\*\*\*|预共享密钥。 |
|RemoteId|String|139.xx.xx.167|对端ID，支持FQDN和IP格式，默认为当前选取的用户网关IP地址。 |
|IpsecConfig|Struct| |第二阶段协商的配置。 |
|IpsecAuthAlg|String|sha1|IPsec认证算法，可选sha1和md5。 |
|IpsecEncAlg|String|aes|IPsec加密算法。 |
|IpsecLifetime|Long|86400|IPsec生存时间。 |
|IpsecPfs|String|group2|DH分组。 |
|RequestId|String|7DB79D0C-5F27-4AB5-995B-79BE55102F90|请求ID。 |
|VcoHealthCheck|Struct| |健康检查配置。 |
|Dip|String|1.1.1.xx|目标IP。 |
|Enable|String|true|是否开启健康检查。

 -   **true**：已开启。
-   **false**：未开启。 |
|Interval|Integer|3|健康检查的重试间隔时间，单位是秒。 |
|Retry|Integer|1|健康检查的重试发包次数。 |
|Sip|String|2.2.2.xx|源IP。 |
|VpnBgpConfig|Struct| |Bgp配置信息。 |
|EnableBgp|String|true|Bgp的开启状态。

 -   **true**：已开启。
-   **false**：未开启。 |
|LocalAsn|Integer|10001|本端自治系统号。 |
|LocalBgpIp|String|169.254.11.1|本端Bgp地址。 |
|PeerAsn|Integer|10002|对端自治系统号。 |
|PeerBgpIp|String|169.254.11.2|对端Bgp地址。 |
|Status|String|success|Bgp的协商状态。

 -   **success**：Bgp正常。
-   **false**：Bgp异常。 |
|TunnelCidr|String|169.254.11.0/30|IPsec隧道网段。 |

## 示例

请求示例

```
https://vpc.aliyuncs.com/?Action=ModifyVpnConnectionAttribute
&RegionId=cn-shanghai
&VpnConnectionId=vco-bp1bbi27hojx80nck****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyVpnConnectionAttributeResponse>
  <LocalSubnet>10.0.0.0/8</LocalSubnet>
  <RequestId>89C9783E-A2D7-4F07-96CF-6C65C0E50BD3</RequestId>
  <CustomerGatewayId>cgw-gw8usu4zsk23pf69f****</CustomerGatewayId>
  <CreateTime>1590495160000</CreateTime>
  <Name>VPN1-CGW22</Name>
  <EffectImmediately>false</EffectImmediately>
  <RemoteSubnet>192.168.0.0/16</RemoteSubnet>
  <VcoHealthCheck>
        <Enable>false</Enable>
        <Dip></Dip>
        <Sip></Sip>
        <Retry>0</Retry>
        <Interval>0</Interval>
  </VcoHealthCheck>
  <VpnGatewayId>vpn-gw8bvv722zwjht7ia****</VpnGatewayId>
  <IpsecConfig>
        <IpsecPfs>group2</IpsecPfs>
        <IpsecEncAlg>aes</IpsecEncAlg>
        <IpsecAuthAlg>sha1</IpsecAuthAlg>
        <IpsecLifetime>86400</IpsecLifetime>
  </IpsecConfig>
  <VpnConnectionId>vco-gw8tylx7hvwhl7tu8****</VpnConnectionId>
  <EnableNatTraversal>true</EnableNatTraversal>
  <EnableDpd>true</EnableDpd>
  <IkeConfig>
        <IkeAuthAlg>sha1</IkeAuthAlg>
        <LocalId>8.xx.xx.192</LocalId>
        <IkeEncAlg>aes</IkeEncAlg>
        <IkeVersion>ikev1</IkeVersion>
        <IkeMode>main</IkeMode>
        <IkeLifetime>86400</IkeLifetime>
        <Psk>123456</Psk>
        <RemoteId>8.xx.xx.146</RemoteId>
        <IkePfs>group2</IkePfs>
  </IkeConfig>
  <VpnBgpConfig>
        <Status>success</Status>
        <EnableBgp>true</EnableBgp>
        <LocalAsn>10001</LocalAsn>
        <TunnelCidr>169.254.10.0/30</TunnelCidr>
        <PeerBgpIp>169.254.10.2</PeerBgpIp>
        <PeerAsn>10002</PeerAsn>
        <LocalBgpIp>169.254.10.1</LocalBgpIp>
  </VpnBgpConfig>
</ModifyVpnConnectionAttributeResponse>
```

`JSON`格式

```
{
	"LocalSubnet": "10.0.0.0/8",
	"RequestId": "89C9783E-A2D7-4F07-96CF-6C65C0E50BD3",
	"CustomerGatewayId": "cgw-gw8usu4zsk23pf69f****",
	"CreateTime": 1590495160000,
	"Name": "VPN1-CGW22",
	"EffectImmediately": false,
	"RemoteSubnet": "192.168.0.0/16",
	"VcoHealthCheck": {
		"Enable": "false",
		"Dip": "",
		"Sip": "",
		"Retry": 0,
		"Interval": 0
	},
	"VpnGatewayId": "vpn-gw8bvv722zwjht7ia****",
	"IpsecConfig": {
		"IpsecPfs": "group2",
		"IpsecEncAlg": "aes",
		"IpsecAuthAlg": "sha1",
		"IpsecLifetime": 86400
	},
	"VpnConnectionId": "vco-gw8tylx7hvwhl7tu8****",
	"EnableNatTraversal": true,
	"EnableDpd": true,
	"IkeConfig": {
		"IkeAuthAlg": "sha1",
		"LocalId": "8.xx.xx.192",
		"IkeEncAlg": "aes",
		"IkeVersion": "ikev1",
		"IkeMode": "main",
		"IkeLifetime": 86400,
		"Psk": "123456",
		"RemoteId": "8.xx.xx.146",
		"IkePfs": "group2"
	},
	"VpnBgpConfig": {
		"Status": "success",
		"EnableBgp": "true",
		"LocalAsn": 10001,
		"TunnelCidr": "169.254.10.0/30",
		"PeerBgpIp": "169.254.10.2",
		"PeerAsn": 10002,
		"LocalBgpIp": "169.254.10.1"
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|404|InvalidVpnConnectionInstanceId.NotFound|The specified vpn connection instance id does not exist.|指定的 VPN 连接不存在，请您检查该 VPN 链接是否正确。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|该服务已欠费，请您先充值再操作。|
|400|InvalidName|The name is not valid|该名称格式不合法。|
|400|QuotaExceeded.PolicyBasedRoute|The maximum number of policy-based routes is exceeded. Existing routes: %s. Routes to be created: %s. Maximum routes: %s.|策略路由条数已达上限，当前已有%s条，本次将创建%s条，上限为%s条。|
|400|IllegalParam.LocalSubnet|The specified "LocalSubnet" \(%s\) is invalid.|本端网段\(%s\)不合法。|
|400|IllegalParam.RemoteSubnet|The specified "RemoteSubnet" \(%s\) is invalid.|对端网段\(%s\)不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

