# DescribeVpnConnections

Queries one or more IPsec-VPN connections.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DescribeVpnConnections&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVpnConnections|The operation that you want to perform. Set the value to **DescribeVpnConnections**. |
|RegionId|String|Yes|cn-hangzhou|The region where the IPsec-VPN connection is deployed.

You can call the [DescribeRegions](~~36063~~) operation to query the region IDs. |
|VpnGatewayId|String|No|vpn-bp1q8bgx4xnkx\*\*\*\*|The ID of the VPN gateway. |
|CustomerGatewayId|String|No|cgw-bp1mvj4g9kogw\*\*\*\*|The ID of the customer gateway. |
|PageNumber|Integer|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: **50**. Default value: **10**. |
|VpnConnectionId|String|No|vco-bp15oes1py4i6\*\*\*\*|The name of the IPsec-VPN connection. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|VpnConnections|Array| |The details of the IPsec-VPN connection. |
|VpnConnection| | | |
|IkeConfig|Struct| |The configurations of Phase 1 negotiations. |
|IkeAuthAlg|String|sha1|The IKE authentication algorithm. |
|IkeEncAlg|String|aes|The IKE encryption algorithm. |
|IkeLifetime|Long|86400|The IKE lifetime. |
|IkeMode|String|main|The IKE mode. Both the main mode and aggressive mode are supported.

The main mode features high security. If NAT traversal is enabled, we recommend that you select the aggressive mode. |
|IkePfs|String|group2|The DH group. |
|IkeVersion|String|ikev1|The IKE version. |
|LocalId|String|116.xx.xx.64|The local ID of the VPN gateway. The default value is the IP address of the VPN gateway. Both fully qualified domain name \(FQDN\) and IP address formats are supported. |
|Psk|String|pgw6dy7dxxxxxxxx|The pre-shared key. |
|RemoteId|String|139.xx.xx.167|The ID of the peer. By default, it is the IP address of the customer gateway. Both FQDN and IP formats are supported. |
|IpsecConfig|Struct| |The configurations for Phase 2 negotiations. |
|IpsecAuthAlg|String|sha1|The IPsec authentication algorithm. |
|IpsecEncAlg|String|aes|The IPsec encryption algorithm. |
|IpsecLifetime|Long|86400|The IPsec lifetime. |
|IpsecPfs|String|group2|The DH group. |
|VpnConnectionId|String|vco-bp10lz7aejumd\*\*\*\*|The ID of the IPsec-VPN connection. |
|CustomerGatewayId|String|vpn-bp1q8bgx4xnk\*\*\*\*|The ID of the customer gateway. |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm\*\*\*\*|The ID of the VPN gateway. |
|Name|String|name|The name of the IPsec-VPN connection. |
|LocalSubnet|String|1.1.1.0/24,1.1.2.0/24|The CIDR block of the VPC. |
|RemoteSubnet|String|1.1.1.0/24,1.1.2.0/24|The CIDR block of the on-premises data center. |
|CreateTime|Long|1492753817000|The time when the IPsec-VPN connection was created. |
|Status|String|ipsec\_sa\_established|The status of the connection.

-   **ike\_sa\_not\_established**: Phase 1 negotiations failed.
-   **ike\_sa\_established**: Phase 1 negotiations were successful.
-   **ipsec\_sa\_not\_established**: Phase 2 negotiations failed.
-   **ipsec\_sa\_established**: Phase 2 negotiations were successful. |
|EffectImmediately|Boolean|true|Indicates whether the connection immediately takes effect.

-   **true**: A reconnection is triggered when the configuration is changed.
-   **false**: Reconnection is triggered when traffic is detected. Reconnections may cause transient connection errors. |
|EnableDpd|Boolean|true|Indicates whether dead peer detection \(DPD\) is enabled.

-   **true**: The DPD feature is enabled.

The IPsec initiator sends DPD packets to verify the existence and availability of IPsec peers. If no feedback is received from the peer within a specified period of time, the IPsec initiator will disconnect the IPsec tunnel. ISAKMP SA and IPsec SA are deleted. The security tunnel is also deleted.

-   **false**: The DPD feature is disabled. The IPsec initiator does not send DPD packets. |
|EnableNatTraversal|Boolean|true|Indicates whether to enable the NAT traversal feature.

-   **true**: The NAT traversal feature is enabled.

After NAT traversal is enabled, the initiator does not need to check the UDP ports during IKE negotiations and can automatically discover NAT gateway devices through the VPN tunnel.

-   **false**: The NAT traversal feature is disabled. |
|VcoHealthCheck|Struct| |The health check configurations. |
|Dip|String|8.xx.xx.8|The destination IP address configured for health checks. |
|Enable|String|true|The status of the health check.

-   **true**: The health check is enabled.
-   **false**: The health check is disabled. |
|Interval|Integer|2|The interval between two consecutive health checks. Unit: seconds. |
|Retry|Integer|3|The number of times that health check packets are resent. |
|Sip|String|192.xx.xx.66|The source IP address configured for health checks. |
|Status|String|success|The result of the health check.

-   **failed**: The health check is not passed.
-   **success**: The health check is passed. |
|VpnBgpConfig|Struct| |BGP configuration information. |
|LocalAsn|String|10001|The local autonomous system number. |
|LocalBgpIp|String|169.254.10.2|The BGP address of the local VPN gateway that belongs to the CIDR block of the IPsec tunnel. |
|PeerAsn|String|10002|The peer autonomous system number. |
|PeerBgpIp|String|169.254.10.1|The BGP address of the peer. It is an IP address within the IPsec tunnel CIDR block. |
|Status|String|success|The BGP status

-   **success**: BGP is in the working state.
-   **false**: BGP failed. |
|TunnelCidr|String|169.254.10.0/30|The CIDR block of the IPsec tunnel. The subnet mask of the CIDR block is 30 bits within 169.254.0.0/16. |
|TotalCount|Integer|10|The total number of entries. |
|PageNumber|Integer|1|The number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|54A4B3D0-DF4D-4C54-B8DC-5DC8DD49C939|The ID of the request. |

## Examples

Sample requests

```
https://vpc.aliyuncs.com/?Action=DescribeVpnConnections
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are not authorized to perform this operation on the specified resource. You can apply for the permission and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are not authorized to perform this operation on the specified resource. To acquire the required permissions, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

