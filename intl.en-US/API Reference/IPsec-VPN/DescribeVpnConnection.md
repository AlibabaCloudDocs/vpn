# DescribeVpnConnection

Queries detailed information about an IPsec-VPN connection.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DescribeVpnConnection&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVpnConnection|The operation that you want to perform. Set the value to **DescribeVpnConnection**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the IPsec-VPN connection is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|VpnConnectionId|String|Yes|vco-bp1bbi27hojx80nck\*\*\*\*|The name of the IPsec-VPN connection. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|VpnConnectionId|String|vco-bp1bbi27hojx80nck\*\*\*\*|The name of the IPsec-VPN connection. |
|CustomerGatewayId|String|cgw-bp1mvj4g9kogwwcxk\*\*\*\*|The ID of the customer gateway. |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the VPN gateway. |
|Name|String|ipsec1|The name of the IPsec-VPN connection. |
|LocalSubnet|String|1.1.1.0/24,1.1.2.0/24|The CIDR block of the virtual private cloud \(VPC\). |
|RemoteSubnet|String|1.1.1.0/24,1.1.2.0/24|The CIDR block of the on-premises data center. |
|CreateTime|Long|1492753817000|The time when the IPsec-VPN connection was created. |
|Status|String|ike\_sa\_not\_established|The status of the IPsec-VPN connection. Valid values:

 -   **ike\_sa\_not\_established**: indicates that Phase 1 negotiations failed.
-   **ike\_sa\_established**: indicates that Phase 1 negotiations succeeded.
-   **ipsec\_sa\_not\_established**: indicates that Phase 2 negotiations failed.
-   **ipsec\_sa\_established**: indicates that Phase 2 negotiations succeeded. |
|EffectImmediately|Boolean|true|Indicates whether IPsec-VPN negotiations are initiated immediately. Valid values:

 -   **true**: Negotiations are initiated when the configuration is changed.
-   **false**: Negotiations are initiated when traffic is detected. Transient connection errors may occur when negotiations are initiated. |
|IkeConfig| | |The configuration of Phase 1 negotiations. |
|IkeAuthAlg|String|sha1|The IKE authentication algorithm. Both SHA-1 and MD5 are supported. |
|IkeEncAlg|String|aes|The IKE encryption algorithm. |
|IkeLifetime|Long|86400|The IKE lifetime. |
|IkeMode|String|main|The IKE mode. Both main and aggressive modes are supported. The main mode offers higher security. If NAT traversal is enabled, we recommend that you select the aggressive mode. |
|IkePfs|String|group2|The DH group. |
|IkeVersion|String|ikev1|The IKE version. |
|LocalId|String|116.62.69.xxx|The ID of the VPN gateway. By default, it is the IP address of the VPN gateway. Both FQDN and IP formats are supported. |
|Psk|String|pgw6dy7d1i8in7x5|The pre-shared key. |
|RemoteId|String|139.196.32.xxx|The ID of the customer gateway. By default, it is the IP address of the customer gateway. Both FQDN and IP formats are supported. |
|IpsecConfig| | |The configuration of Phase 2 negotiations. |
|IpsecAuthAlg|String|sha1|The IPsec authentication algorithm. Both SHA-1 and MD5 are supported. |
|IpsecEncAlg|String|aes|The IPsec encryption algorithm. |
|IpsecLifetime|Long|86400|The IPsec lifetime. |
|IpsecPfs|String|group2|The DH group. |
|RequestId|String|F2310D45-BCF6-4E2E-9082-B4503844BA4C|The ID of the request. |
|VcoHealthCheck| | |Information about health checks. |
|Dip|String|10.0.0.xx|The destination IP address. |
|Enable|String|true|Indicates whether health checks are enabled. Valid values:

 -   **false**: indicates that health checks are disabled.
-   **true**: indicates that health checks are enabled. |
|Interval|Integer|3|The interval between two consecutive health checks. Unit: seconds. |
|Retry|Integer|3|The maximum number of health check retries. |
|Sip|String|192.168.1.xx|The source IP address. |
|Status|String|failed|The status of the health check. Valid values: |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=DescribeVpnConnection
&RegionId=cn-hangzhou
&VpnConnectionId=vco-bp1bbi27hojx80nck****
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DescribeVpnConnectionResponse>
      <PageNumber>1</PageNumber>
      <VpnConnections>
            <VpnConnection>
                  <Name>c2</Name>
                  <CustomerGatewayId>cgw-bp1wl8dtz3auwlav****</CustomerGatewayId>
                  <Status>ike_sa_not_established</Status>
                  <RemoteSubnet>192.168.0.0/16</RemoteSubnet>
                  <IpsecConfig>
                        <IpsecLifetime>86400</IpsecLifetime>
                        <IpsecAuthAlg>md5</IpsecAuthAlg>
                        <IpsecPfs>group2</IpsecPfs>
                        <IpsecEncAlg>aes</IpsecEncAlg>
                  </IpsecConfig>
                  <EffectImmediately>false</EffectImmediately>
                  <VpnGatewayId>vpn-bp1yfrjxn4d5t63tb****</VpnGatewayId>
                  <CreateTime>1519391420000</CreateTime>
                  <VpnConnectionId>vco-bp1w3m1p23iftycvs****</VpnConnectionId>
                  <LocalSubnet>172.16.0.0/12</LocalSubnet>
                  <IkeConfig>
                        <IkeEncAlg>aes</IkeEncAlg>
                        <RemoteId>47.97.176.xxx</RemoteId>
                        <IkePfs>group2</IkePfs>
                        <IkeAuthAlg>sha1</IkeAuthAlg>
                        <Psk>1234567</Psk>
                        <IkeMode>aggressive</IkeMode>
                        <IkeLifetime>86400</IkeLifetime>
                        <IkeVersion>ikev1</IkeVersion>
                        <LocalId>116.62.119.xxx</LocalId>
                  </IkeConfig>
            </VpnConnection>
      </VpnConnections>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>7D598A10-26EF-44F2-9F47-E417842F3CEA</RequestId>
</DescribeVpnConnectionResponse>
```

`JSON` format

```
{
	"PageNumber":1,
	"VpnConnections":{
		"VpnConnection":[
			{
				"CustomerGatewayId":"cgw-bp1wl8dtz3auwlavw****",
				"Name":"c2",
				"Status":"ike_sa_not_established",
				"RemoteSubnet":"192.168.0.0/16",
				"IpsecConfig":{
					"IpsecLifetime":86400,
					"IpsecAuthAlg":"md5",
					"IpsecPfs":"group2",
					"IpsecEncAlg":"aes"
				},
				"VpnGatewayId":"vpn-bp1yfrjxn4d5t63t****",
				"EffectImmediately":false,
				"VpnConnectionId":"vco-bp1w3m1p23iftycv****",
				"CreateTime":1519391420000,
				"LocalSubnet":"172.16.0.0/12",
				"IkeConfig":{
					"IkeEncAlg":"aes",
					"IkePfs":"group2",
					"RemoteId":"47.97.176.xxx",
					"IkeAuthAlg":"sha1",
					"Psk":"1234567",
					"IkeMode":"aggressive",
					"IkeLifetime":86400,
					"IkeVersion":"ikev1",
					"LocalId":"116.62.119.xxx"
				}
			}
		]
	},
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"7D598A10-26EF-44F2-9F47-E417842F3CEA"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. You can apply for the permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|404|InvalidVpnConnectionInstanceId.NotFound|The specified vpn connection instance id does not exist.|The error message returned because the specified IPsec-VPN connection does not exist. You can check whether the configuration of the connection is valid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

