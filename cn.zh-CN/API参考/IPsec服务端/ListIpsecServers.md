# ListIpsecServers

调用ListIpsecServers查看已创建的IPsec服务端。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=ListIpsecServers&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListIpsecServers|要执行的操作。取值：**ListIpsecServers**。 |
|RegionId|String|是|cn-hangzhou|IPsec服务端所属地域ID。 |
|IpsecServerId.N|RepeatList|否|iss-bp1bo3xuvcxo7ixll\*\*\*\*|IPsec服务端ID。 |
|IpsecServerName|String|否|test|IPsec服务端名称。 |
|VpnGatewayId|String|否|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关的ID。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a\*\*\*\*|查询凭证（Token），取值为上一次API调用返回的**NextToken**参数值。如果没有下一个查询，请不传该参数。 |
|MaxResults|Integer|否|10|分页大小，取值范围：**1**~**20**，默认为**10**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|IpsecServers|Array of IpsecServer| |IPsec服务端信息列表。 |
|ClientIpPool|String|10.XX.XX.0/24|客户端网段，指给客户端虚拟网卡分配访问地址的的地址段。 |
|CreationTime|String|2018-12-03T10:11:55Z|IPsec服务端创建时间。

 T表示分隔符，Z表示的是UTC，即世界标准时间。 |
|EffectImmediately|Boolean|false|是否删除当前已协商成功的IPsec隧道并重新发起协商。

 -   **true**：配置完成后立即进行协商。
-   **false**（默认值）：当有流量进入时进行协商。 |
|IDaaSInstanceId|String|idaas-cn-hangzhou-\*\*\*\*|IDaaS实例ID。 |
|IkeConfig|Struct| |第一阶段协商的配置。 |
|IkeAuthAlg|String|sha1|IKE认证算法。 |
|IkeEncAlg|String|aes|IKE加密算法。 |
|IkeLifetime|Long|86400|IKE生存时间。单位：秒。 |
|IkeMode|String|main|IKE版本协商模式。 |
|IkePfs|String|group2|Diffie-Hellman密钥交换算法。 |
|IkeVersion|String|ikev2|IKE版本。 |
|LocalId|String|116.XX.XX.64|IPsec服务端标识符。支持FQDN和IP地址格式，默认为当前选取的VPN网关公网IP地址。 |
|RemoteId|String|139.XX.XX.167|对端标识符。支持FQDN和IP地址格式，默认为空。 |
|InternetIp|String|47.XX.XX.246|VPN网关公网IP地址。 |
|IpsecConfig|Struct| |第二阶段协商的配置。 |
|IpsecAuthAlg|String|sha1|IPsec认证算法。 |
|IpsecEncAlg|String|aes|IPsec加密算法。 |
|IpsecLifetime|Long|86400|IPsec生存时间。单位：秒。 |
|IpsecPfs|String|group2|Diffie-Hellman密钥交换算法。 |
|IpsecServerId|String|iss-bp1bo3xuvcxo7ixll\*\*\*\*|IPsec服务端ID。 |
|IpsecServerName|String|test|IPsec服务端名称。 |
|LocalSubnet|String|1.XX.XX.0/24,1.XX.XX.0/24|本端网段，指需要和客户端网段互连的VPC侧的网段。 |
|MaxConnections|Integer|5|VPN网关的SSL连接数规格。

 **说明：** SSL-VPN与IPsec服务端共享SSL连接数。例如，SSL连接数为5，您已经有3个SSL客户端连接了SSL-VPN，则您还能使用2个客户端连接IPsec服务端。 |
|MultiFactorAuthEnabled|Boolean|true|是否已开启双因子认证功能。

 -   **true**：已开启。
-   **false**：未开启。 |
|OnlineClientCount|Integer|1|已经连接IPsec服务端的客户端数量。 |
|Psk|String|pgw6dy7d\*\*\*\*|预共享密钥。 |
|PskEnabled|Boolean|true|是否开启预共享密钥认证方式。仅取值为**true**，表示开启预共享密钥认证方式。 |
|RegionId|String|cn-hangzhou|IPsec服务端所属地域ID。 |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关的ID。 |
|MaxResults|Integer|1|分页大小。 |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a\*\*\*\*|下一次查询凭证（Token）。 |
|RequestId|String|54B48E3D-DF70-471B-AA93-08E683A1B457|请求ID。 |
|TotalCount|Integer|10|列表条目数。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListIpsecServers
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListIpsecServersResponse>
  <TotalCount>1</TotalCount>
  <IpsecServers>
        <LocalSubnet>192.168.1.0/24</LocalSubnet>
        <ClientIpPool>10.1.1.0/24</ClientIpPool>
        <MultiFactorAuthEnabled>false</MultiFactorAuthEnabled>
        <MaxConnections>10</MaxConnections>
        <IpsecServerId>iss-bp1bo3xuvcxo7ixll****</IpsecServerId>
        <Psk>so7suwy****</Psk>
        <PskEnabled>true</PskEnabled>
        <EffectImmediately>false</EffectImmediately>
        <InternetIp>47.XX.XX.246</InternetIp>
        <VpnGatewayId>vpn-bp17lofy9fd0****</VpnGatewayId>
        <OnlineClientCount>0</OnlineClientCount>
        <IpsecConfig>
              <IpsecPfs>group2</IpsecPfs>
              <IpsecEncAlg>aes</IpsecEncAlg>
              <IpsecAuthAlg>sha1</IpsecAuthAlg>
              <IpsecLifetime>86400</IpsecLifetime>
        </IpsecConfig>
        <CreationTime>2021-02-22T07:54:38Z</CreationTime>
        <RegionId>cn-hangzhou</RegionId>
        <IkeConfig>
              <IkeAuthAlg>sha1</IkeAuthAlg>
              <LocalId>47.XX.XX.246</LocalId>
              <IkeEncAlg>aes</IkeEncAlg>
              <IkeVersion>ikev2</IkeVersion>
              <IkeMode>main</IkeMode>
              <IkeLifetime>86400</IkeLifetime>
              <IkePfs>group2</IkePfs>
        </IkeConfig>
  </IpsecServers>
  <RequestId>66881D3C-07C1-402A-991E-26830E867B01</RequestId>
  <MaxResults>10</MaxResults>
</ListIpsecServersResponse>
```

`JSON`格式

```
{
  "TotalCount": 1,
  "IpsecServers": [
    {
      "LocalSubnet": "192.168.1.0/24",
      "ClientIpPool": "10.1.1.0/24",
      "MultiFactorAuthEnabled": false,
      "MaxConnections": 10,
      "IpsecServerId": "iss-bp1bo3xuvcxo7ixll****",
      "Psk": "so7suwy****",
      "PskEnabled": true,
      "EffectImmediately": false,
      "InternetIp": "47.XX.XX.246",
      "VpnGatewayId": "vpn-bp17lofy9fd0****",
      "OnlineClientCount": 0,
      "IpsecConfig": {
        "IpsecPfs": "group2",
        "IpsecEncAlg": "aes",
        "IpsecAuthAlg": "sha1",
        "IpsecLifetime": 86400
      },
      "CreationTime": "2021-02-22T07:54:38Z",
      "RegionId": "cn-hangzhou",
      "IkeConfig": {
        "IkeAuthAlg": "sha1",
        "LocalId": "47.XX.XX.246",
        "IkeEncAlg": "aes",
        "IkeVersion": "ikev2",
        "IkeMode": "main",
        "IkeLifetime": 86400,
        "IkePfs": "group2"
      }
    }
  ],
  "RequestId": "66881D3C-07C1-402A-991E-26830E867B01",
  "MaxResults": 10
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

