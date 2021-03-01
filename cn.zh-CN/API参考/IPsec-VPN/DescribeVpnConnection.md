# DescribeVpnConnection

调用DescribeVpnConnection接口查询已创建的IPsec连接的详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DescribeVpnConnection&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVpnConnection|要执行的操作，取值：**DescribeVpnConnection**。 |
|RegionId|String|是|cn-hangzhou|IPsec连接所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpnConnectionId|String|是|vco-bp1bbi27hojx80nck\*\*\*\*|IPsec连接的ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|VpnConnectionId|String|vco-bp1bbi27hojx80nck\*\*\*\*|IPsec连接的ID。 |
|CustomerGatewayId|String|cgw-bp1mvj4g9kogwwcxk\*\*\*\*|用户网关的ID。 |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关的ID。 |
|Name|String|ipsec1|IPsec连接的名称。 |
|LocalSubnet|String|1.1.1.0/24|VPC侧的网段。 |
|RemoteSubnet|String|1.1.1.0/24|本地IDC侧的网段。 |
|CreateTime|Long|1492753817000|创建IPsec连接时间戳。 |
|Status|String|ike\_sa\_not\_established|连接状态。

 -   **ike\_sa\_not\_established**：第一阶段协商失败。
-   **ike\_sa\_established**：第一阶段协商成功。
-   **ipsec\_sa\_not\_established**：第二阶段协商失败。
-   **ipsec\_sa\_established**：第二阶段协商成功。 |
|EffectImmediately|Boolean|true|IPsec连接是否立即生效。

 -   **true**：配置变更时触发重连。
-   **false**：有流量时触发重连。重连有可能导致流量闪断。 |
|EnableDpd|Boolean|true|是否开启DPD（对等体存活检测）功能。

 -   **false**：未开启。
-   **true**：已开启。

 开启DPD功能后，IPsec发起端会发送DPD报文用来检测对端的设备是否存活，如果在设定时间内未收到正确回应则认为对端已经断线，IPsec将删除ISAKMP SA和相应的IPsec SA，安全隧道同样也会被删除。 |
|EnableNatTraversal|Boolean|true|是否开启NAT穿越功能。

 -   **true**：开启NAT穿越功能。
-   **false**：不开启NAT穿越功能。

 开启NAT穿越功能后，IKE协商过程会删除对UDP端口号的验证过程，同时实现对VPN隧道中NAT网关设备的发现功能。 |
|IkeConfig|Struct| |第一阶段协商的配置。 |
|IkeAuthAlg|String|sha1|IKE认证算法。 |
|IkeEncAlg|String|aes|IKE加密算法。 |
|IkeLifetime|Long|86400|IKE生存时间。单位：秒。 |
|IkeMode|String|main|IKE协商模式。 |
|IkePfs|String|group2|DH分组。 |
|IkeVersion|String|ikev1|IKE协议版本。 |
|LocalId|String|116.XX.XX.6|本端标识符。支持FQDN和IP地址格式，默认为当前选取的VPN网关IP地址。 |
|Psk|String|pgw6dy\*\*\*\*|预共享密钥。 |
|RemoteId|String|139.XX.XX.6|对端标识符。支持FQDN和IP地址格式，默认为当前选取的用户网关IP地址。 |
|IpsecConfig|Struct| |第二阶段协商的配置。 |
|IpsecAuthAlg|String|sha1|IPsec认证算法。 |
|IpsecEncAlg|String|aes|IPsec加密算法。 |
|IpsecLifetime|Long|86400|IPsec生存时间。单位：秒。 |
|IpsecPfs|String|group2|DH分组。 |
|RemoteCaCertificate|String|-----BEGIN CERTIFICATE----- MIIB7zCCAZW\*\*\*\*|对端的CA证书。 |
|RequestId|String|F2310D45-BCF6-4E2E-9082-B4503844BA4C|请求ID。 |
|VcoHealthCheck|Struct| |健康检查信息。 |
|Dip|String|10.0.0.1|目标IP地址。 |
|Enable|String|true|是否已开启健康检查。

 -   **false**：未开启。
-   **true**：已开启。 |
|Interval|Integer|3|健康检查的重试间隔时间，单位：秒。 |
|Retry|Integer|3|健康检查的重试发包次数。 |
|Sip|String|192.168.1.1|源IP地址。 |
|Status|String|failed|健康检查状态。

 -   **failed**：异常。
-   **success**：正常。 |
|VpnBgpConfig|Struct| |Bgp配置信息。 |
|EnableBgp|String|true|Bgp的开启状态。

 -   **true**：已开启。
-   **false**：未开启。 |
|LocalAsn|String|45014|本端自治系统号。 |
|LocalBgpIp|String|169.254.XX.XX|本端Bgp地址。 |
|PeerAsn|String|65535|对端自治系统号。 |
|PeerBgpIp|String|169.254.XX.XX|对端Bgp地址。 |
|Status|String|true|Bgp的协商状态。

 -   **success**：Bgp正常。
-   **false**：Bgp异常。 |
|TunnelCidr|String|169.254.11.0/30|IPsec隧道网段。该网段是一个在169.254.0.0/16内的掩码长度为30的网段。 |

## 示例

请求示例

```
https://vpc.aliyuncs.com/?Action=DescribeVpnConnection
&RegionId=cn-hangzhou
&VpnConnectionId=vco-bp1bbi27hojx80nck****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeVpnConnectionResponse>
  <LocalSubnet>10.0.0.0/8</LocalSubnet>
  <Status>ipsec_sa_established</Status>
  <RequestId>6FBAE985-A938-49CB-9129-621AA3A88728</RequestId>
  <CustomerGatewayId>cgw-gw8usu4zsk23pf69f****</CustomerGatewayId>
  <CreateTime>1590495160000</CreateTime>
  <Name>VPN1-CGW22</Name>
  <EffectImmediately>false</EffectImmediately>
  <RemoteSubnet>192.168.0.0/16</RemoteSubnet>
  <VcoHealthCheck>
        <Status>success</Status>
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
        <LocalId>8.XX.XX.192</LocalId>
        <IkeEncAlg>aes</IkeEncAlg>
        <IkeVersion>ikev1</IkeVersion>
        <IkeMode>main</IkeMode>
        <IkeLifetime>86400</IkeLifetime>
        <Psk>123456</Psk>
        <RemoteId>8.XX.XX.146</RemoteId>
        <IkePfs>group2</IkePfs>
  </IkeConfig>
  <VpnBgpConfig>
        <Status>success</Status>
        <EnableBgp>true</EnableBgp>
        <LocalAsn>45104</LocalAsn>
        <TunnelCidr>169.254.10.0/30</TunnelCidr>
        <PeerBgpIp>169.254.XX.XX</PeerBgpIp>
        <PeerAsn>65535</PeerAsn>
        <LocalBgpIp>169.254.XX.XX</LocalBgpIp>
  </VpnBgpConfig>
</DescribeVpnConnectionResponse>
```

`JSON`格式

```
{
	"LocalSubnet": "10.0.0.0/8",
	"Status": "ipsec_sa_established",
	"RequestId": "6FBAE985-A938-49CB-9129-621AA3A88728",
	"CustomerGatewayId": "cgw-gw8usu4zsk23pf69f****",
	"CreateTime": 1590495160000,
	"Name": "VPN1-CGW22",
	"EffectImmediately": false,
	"RemoteSubnet": "192.168.0.0/16",
	"VcoHealthCheck": {
		"Status": "success",
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
		"LocalId": "8.XX.XX.192",
		"IkeEncAlg": "aes",
		"IkeVersion": "ikev1",
		"IkeMode": "main",
		"IkeLifetime": 86400,
		"Psk": "123456",
		"RemoteId": "8.XX.XX.146",
		"IkePfs": "group2"
	},
	"VpnBgpConfig": {
		"Status": "success",
		"EnableBgp": "true",
		"LocalAsn": 45104,
		"TunnelCidr": "169.254.10.0/30",
		"PeerBgpIp": "169.254.XX.XX",
		"PeerAsn": 65535,
		"LocalBgpIp": "169.254.XX.XX"
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|404|InvalidVpnConnectionInstanceId.NotFound|The specified vpn connection instance id does not exist.|指定的 VPN 连接不存在，请您检查该 VPN 链接是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

