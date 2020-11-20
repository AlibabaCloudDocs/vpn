# DescribeVpnConnections

调用DescribeVpnConnections接口查询已创建的IPsec连接。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DescribeVpnConnections&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVpnConnections|要执行的操作，取值：**DescribeVpnConnections**。 |
|RegionId|String|是|cn-hangzhou|IPsec连接所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpnGatewayId|String|否|vpn-bp1q8bgx4xnkx\*\*\*\*|VPN网关的ID。 |
|CustomerGatewayId|String|否|cgw-bp1mvj4g9kogw\*\*\*\*|用户网关的ID。 |
|PageNumber|Integer|否|1|列表的页码，默认值为**1**。 |
|PageSize|Integer|否|10|分页查询时每页的行数，最大值为**50**，默认值为**10**。 |
|VpnConnectionId|String|否|vco-bp15oes1py4i6\*\*\*\*|IPsec连接的ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|VpnConnections|Array| |IPsec连接列表的详细信息。 |
|VpnConnection| | | |
|IkeConfig|Struct| |第一阶段协商的配置。 |
|IkeAuthAlg|String|sha1|IKE认证算法。 |
|IkeEncAlg|String|aes|IKE加密算法。 |
|IkeLifetime|Long|86400|IKE生存时间。 |
|IkeMode|String|main|IKE模式，可选main和aggressive模式。

 main模式安全性高，如果启用了NAT穿越，建议选择aggressive模式。 |
|IkePfs|String|group2|DH分组。 |
|IkeVersion|String|ikev1|IKE版本。 |
|LocalId|String|116.xx.xx.64|本端ID，支持FQDN和IP格式，默认为当前选取的VPN网关IP地址。 |
|Psk|String|pgw6dy7dxxxxxxxx|预共享密钥。 |
|RemoteId|String|139.xx.xx.167|对端ID，支持FQDN和IP格式，默认为当前选取的用户网关IP地址。 |
|IpsecConfig|Struct| |第二阶段协商的配置。 |
|IpsecAuthAlg|String|sha1|IPsec认证算法。 |
|IpsecEncAlg|String|aes|IPsec加密算法。 |
|IpsecLifetime|Long|86400|IPsec生存时间。 |
|IpsecPfs|String|group2|DH分组。 |
|VpnConnectionId|String|vco-bp10lz7aejumd\*\*\*\*|IPsec连接的ID。 |
|CustomerGatewayId|String|vpn-bp1q8bgx4xnk\*\*\*\*|用户网关的ID。 |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm\*\*\*\*|VPN网关的ID。 |
|Name|String|name|IPsec连接的名称。 |
|LocalSubnet|String|1.1.1.0/24,1.1.2.0/24|VPC侧的网段。 |
|RemoteSubnet|String|1.1.1.0/24,1.1.2.0/24|本地IDC侧的网段。 |
|CreateTime|Long|1492753817000|IPsec连接的创建时间。 |
|Status|String|ipsec\_sa\_established|连接状态。

 -   **ike\_sa\_not\_established**：第一阶段协商失败。
-   **ike\_sa\_established**：第一阶段协商成功。
-   **ipsec\_sa\_not\_established**：第二阶段协商失败。
-   **ipsec\_sa\_established**：第二阶段协商成功。 |
|EffectImmediately|Boolean|true|是否立即生效。

 -   **是**：配置变更时触发重连。
-   **否**：有流量时触发重连。重连有可能导致流量闪断。 |
|EnableDpd|Boolean|true|是否开启DPD（对等体存活检测）功能。

 -   **true**：开启DPD功能。

IPsec发起端会发送DPD报文用来检测对端的设备是否存活，如果在设定时间内未收到正确回应则认为对端已经断线，IPsec将删除ISAKMP SA和相应的IPsec SA，安全隧道同样也会被删除。

-   **false**：不开启DPD功能，IPsec发起端不会发送DPD探测报文。 |
|EnableNatTraversal|Boolean|true|是否开启NAT穿越功能。

 -   **true**：开启NAT穿越功能。

开启后，IKE协商过程会删除对UDP端口号的验证过程，同时实现对VPN隧道中NAT网关设备的发现功能。

-   **false**：不开启NAT穿越功能。 |
|VcoHealthCheck|Struct| |健康检查配置。 |
|Dip|String|8.xx.xx.8|目的IP地址。 |
|Enable|String|true|健康检查的开启状态。

 -   **true**：已开启。
-   **false**：未开启。 |
|Interval|Integer|2|健康检查的时间间隔。 |
|Retry|Integer|3|健康检查的重试发包次数。 |
|Sip|String|192.xx.xx.66|源IP地址。 |
|Status|String|success|健康检查状态。

 -   **failed**：异常。
-   **success**：正常。 |
|VpnBgpConfig|Struct| |Bgp配置。 |
|LocalAsn|String|10001|本端自治系统号。 |
|LocalBgpIp|String|169.254.10.2|本端Bgp地址，该地址为IPsec隧道网段内的一个IP地址。 |
|PeerAsn|String|10002|对端自治系统号。 |
|PeerBgpIp|String|169.254.10.1|对端Bgp地址，该地址为IPsec隧道网段内的一个IP地址。 |
|Status|String|success|Bgp状态。

 -   **success**：Bgp正常。
-   **false**：Bgp异常。 |
|TunnelCidr|String|169.254.10.0/30|IPsec隧道网段，该网段在169.254.0.0/16内的掩码长度为30的网段。 |
|TotalCount|Integer|10|列表条条目数。 |
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|10|每页包含多少条目。 |
|RequestId|String|54A4B3D0-DF4D-4C54-B8DC-5DC8DD49C939|请求ID。 |

## 示例

请求示例

```
https://vpc.aliyuncs.com/?Action=DescribeVpnConnections
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeVpnConnections>
  <TotalCount>2</TotalCount>
  <RequestId>238752DC-0693-49BE-9C85-711D5691D3E5</RequestId>
  <PageSize>10</PageSize>
  <PageNumber>1</PageNumber>
  <VpnConnections>
        <VpnConnection>
              <LocalSubnet>10.0.0.0/8</LocalSubnet>
              <Status>ipsec_sa_established</Status>
              <CustomerGatewayId>cgw-gw8usu4zsk23pf69f****</CustomerGatewayId>
              <CreateTime>1590495160000</CreateTime>
              <Name>VPN1-CGW22</Name>
              <EffectImmediately>false</EffectImmediately>
              <RemoteSubnet>192.168.0.0/16</RemoteSubnet>
              <VcoHealthCheck>
                    <Status>failed</Status>
                    <Enable>true</Enable>
                    <Dip>192.168.0.1</Dip>
                    <Sip>192.168.0.2</Sip>
                    <Retry>2</Retry>
                    <Interval>2</Interval>
              </VcoHealthCheck>
              <VpnGatewayId>vpn-gw8bvv722zwjht7ia****</VpnGatewayId>
              <IpsecConfig>
                    <IpsecPfs>group2</IpsecPfs>
                    <IpsecEncAlg>aes</IpsecEncAlg>
                    <IpsecAuthAlg>sha1</IpsecAuthAlg>
                    <IpsecLifetime>86400</IpsecLifetime>
              </IpsecConfig>
              <VpnConnectionId>vco-gw8tylx7hvwhl7tu8****</VpnConnectionId>
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
                    <LocalAsn>10001</LocalAsn>
                    <TunnelCidr>169.254.10.0/30</TunnelCidr>
                    <PeerBgpIp>169.254.10.2</PeerBgpIp>
                    <PeerAsn>10001</PeerAsn>
                    <LocalBgpIp>169.254.10.1</LocalBgpIp>
              </VpnBgpConfig>
        </VpnConnection>
        <VpnConnection>
              <LocalSubnet>192.168.0.0/16</LocalSubnet>
              <Status>ipsec_sa_established</Status>
              <CustomerGatewayId>cgw-gw819u3zrifo8m5iz****</CustomerGatewayId>
              <CreateTime>1590495260000</CreateTime>
              <Name>VPN2-CGW1</Name>
              <EffectImmediately>false</EffectImmediately>
              <RemoteSubnet>10.0.0.0/8</RemoteSubnet>
              <VcoHealthCheck>
                    <Status>success</Status>
                    <Enable>true</Enable>
                    <Dip>192.168.0.1</Dip>
                    <Sip>192.168.0.56</Sip>
                    <Retry>2</Retry>
                    <Interval>2</Interval>
              </VcoHealthCheck>
              <VpnGatewayId>vpn-gw8uofjyg2db32o89****</VpnGatewayId>
              <IpsecConfig>
                    <IpsecPfs>group2</IpsecPfs>
                    <IpsecEncAlg>aes</IpsecEncAlg>
                    <IpsecAuthAlg>sha1</IpsecAuthAlg>
                    <IpsecLifetime>86400</IpsecLifetime>
              </IpsecConfig>
              <VpnConnectionId>vco-gw837v1ybfh74b6dy****</VpnConnectionId>
              <IkeConfig>
                    <IkeAuthAlg>sha1</IkeAuthAlg>
                    <LocalId>8.xx.xx.146</LocalId>
                    <IkeEncAlg>aes</IkeEncAlg>
                    <IkeVersion>ikev1</IkeVersion>
                    <IkeMode>main</IkeMode>
                    <IkeLifetime>86400</IkeLifetime>
                    <Psk>123456</Psk>
                    <RemoteId>8.xx.xx.192</RemoteId>
                    <IkePfs>group2</IkePfs>
              </IkeConfig>
              <VpnBgpConfig>
                    <Status>success</Status>
                    <LocalAsn>10001</LocalAsn>
                    <TunnelCidr>169.254.10.0/30</TunnelCidr>
                    <PeerBgpIp>169.254.10.1</PeerBgpIp>
                    <PeerAsn>10001</PeerAsn>
                    <LocalBgpIp>169.254.10.2</LocalBgpIp>
              </VpnBgpConfig>
        </VpnConnection>
  </VpnConnections>
</DescribeVpnConnections>
```

`JSON` 格式

```
{
	"TotalCount": 2,
	"RequestId": "238752DC-0693-49BE-9C85-711D5691D3E5",
	"PageSize": 10,
	"PageNumber": 1,
	"VpnConnections": {
		"VpnConnection": [
			{
				"LocalSubnet": "10.0.0.0/8",
				"Status": "ipsec_sa_established",
				"CustomerGatewayId": "cgw-gw8usu4zsk23pf69f****",
				"CreateTime": 1590495160000,
				"Name": "VPN1-CGW22",
				"EffectImmediately": false,
				"RemoteSubnet": "192.168.0.0/16",
				"VcoHealthCheck": {
					"Status": "failed",
					"Enable": "true",
					"Dip": "192.168.0.1",
					"Sip": "192.168.0.2",
					"Retry": 2,
					"Interval": 2
				},
				"VpnGatewayId": "vpn-gw8bvv722zwjht7ia****",
				"IpsecConfig": {
					"IpsecPfs": "group2",
					"IpsecEncAlg": "aes",
					"IpsecAuthAlg": "sha1",
					"IpsecLifetime": 86400
				},
				"VpnConnectionId": "vco-gw8tylx7hvwhl7tu8****",
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
					"LocalAsn": 10001,
					"TunnelCidr": "169.254.10.0/30",
					"PeerBgpIp": "169.254.10.2",
					"PeerAsn": 10001,
					"LocalBgpIp": "169.254.10.1"
				}
			},
			{
				"LocalSubnet": "192.168.0.0/16",
				"Status": "ipsec_sa_established",
				"CustomerGatewayId": "cgw-gw819u3zrifo8m5iz****",
				"CreateTime": 1590495260000,
				"Name": "VPN2-CGW1",
				"EffectImmediately": false,
				"RemoteSubnet": "10.0.0.0/8",
				"VcoHealthCheck": {
					"Status": "success",
					"Enable": "true",
					"Dip": "192.168.0.1",
					"Sip": "192.168.0.56",
					"Retry": 2,
					"Interval": 2
				},
				"VpnGatewayId": "vpn-gw8uofjyg2db32o89****",
				"IpsecConfig": {
					"IpsecPfs": "group2",
					"IpsecEncAlg": "aes",
					"IpsecAuthAlg": "sha1",
					"IpsecLifetime": 86400
				},
				"VpnConnectionId": "vco-gw837v1ybfh74b6dy****",
				"IkeConfig": {
					"IkeAuthAlg": "sha1",
					"LocalId": "8.xx.xx.146",
					"IkeEncAlg": "aes",
					"IkeVersion": "ikev1",
					"IkeMode": "main",
					"IkeLifetime": 86400,
					"Psk": "123456",
					"RemoteId": "8.xx.xx.192",
					"IkePfs": "group2"
				},
				"VpnBgpConfig": {
					"Status": "success",
					"LocalAsn": 10001,
					"TunnelCidr": "169.254.10.0/30",
					"PeerBgpIp": "169.254.10.1",
					"PeerAsn": 10001,
					"LocalBgpIp": "169.254.10.2"
				}
			}
		]
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Vpc)查看更多错误码。

