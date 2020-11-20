# DownloadVpnConnectionConfig

Queries an IPsec-VPN connection.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DownloadVpnConnectionConfig&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DownloadVpnConnectionConfig|The operation that you want to perform. Set the value to **DownloadVpnConnectionConfig**. |
|RegionId|String|Yes|cn-shanghai|The ID of the region where the IPsec-VPN connection is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|VpnConnectionId|String|Yes|vco-bp1bbi27hojx80nck\*\*\*\*|The ID of the IPsec-VPN connection. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|0C68048B-0F70-40DA-B8AE-1B79B5CF62E3|The ID of the request. |
|VpnConnectionConfig| | |The configuration of the IPsec-VPN connection. |
|IkeConfig| | |The IKE configuration. |
|IkeAuthAlg|String|sha1|The IKE authentication algorithm. Both SHA-1 and MD5 are supported. |
|IkeEncAlg|String|aes|The IKE encryption algorithm. |
|IkeLifetime|Long|86400|The IKE lifetime. |
|IkeMode|String|main|The IKE mode. Both main and aggressive modes are supported. The main mode offers higher security. If NAT traversal is enabled, we recommend that you select the aggressive mode. |
|IkePfs|String|group2|The DH group. |
|IkeVersion|String|ikev1|The IKE version. |
|LocalId|String|116.62.69.xx|The ID of the local VPN gateway. By default, it is the IP address of the VPN gateway. Both FQDN and IP formats are supported. |
|Psk|String|pgw6dy7d1i8i\*\*\*\*|The pre-shared key. |
|RemoteId|String|139.196.32.xx|The ID of the peering VPN gateway. By default, it is the IP address of the customer gateway. Both FQDN and IP formats are supported. |
|IpsecConfig| | |The configuration of the IPsec-VPN connection. |
|IpsecAuthAlg|String|sha1|The IPsec authentication algorithm. Both SHA-1 and MD5 are supported. |
|IpsecEncAlg|String|aes|The IPsec encryption algorithm. |
|IpsecLifetime|Long|86400|The IPsec lifetime. |
|IpsecPfs|String|group2|The DH group. |
|Local|String|139.196.32.xx|The ID of the VPN gateway. |
|LocalSubnet|String|1.1.1.0/24,1.1.2.0/24|The CIDR block of the virtual private cloud \(VPC\). |
|Remote|String|116.62.69.xx|The ID of the customer gateway. |
|RemoteSubnet|String|1.1.1.0/24,1.1.2.0/24|The CIDR block of the on-premises data center. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=DownloadVpnConnectionConfig
&RegionId=cn-shanghai
&VpnConnectionId=vco-bp1bbi27hojx80nck****
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DownloadVpnConnectionConfigResponse>
      <RequestId>6F4A035F-7060-45D7-B9BD-719372782AF6</RequestId>
      <VpnConnectionConfig>
            <RemoteSubnet>1.1.1.0/24,1.1.2.0/24</RemoteSubnet>
            <Local>139.196.32.xx</Local>
            <IpsecConfig>
                  <IpsecLifetime>86400</IpsecLifetime>
                  <IpsecAuthAlg>sha1</IpsecAuthAlg>
                  <IpsecPfs>group2</IpsecPfs>
                  <IpsecEncAlg>aes</IpsecEncAlg>
            </IpsecConfig>
            <Remote>116.62.69.xx</Remote>
            <LocalSubnet>2.2.2.0/24</LocalSubnet>
            <IkeConfig>
                  <IkeEncAlg>aes</IkeEncAlg>
                  <IkePfs>group2</IkePfs>
                  <RemoteId>116.62.69.xx</RemoteId>
                  <IkeAuthAlg>sha1</IkeAuthAlg>
                  <Psk>pgw6dy7d1i8i****</Psk>
                  <IkeMode>main</IkeMode>
                  <IkeLifetime>86400</IkeLifetime>
                  <IkeVersion>ikev1</IkeVersion>
                  <LocalId>139.196.32.xx</LocalId>
            </IkeConfig>
      </VpnConnectionConfig>
</DownloadVpnConnectionConfigResponse>
```

`JSON` format

```
{
	"RequestId":"0C68048B-0F70-40DA-B8AE-1B79B5CF62E3",
	"VpnConnectionConfig":{
		"RemoteSubnet":"1.1.1.0/24,1.1.2.0/24",
		"IpsecConfig":{
			"IpsecLifetime":86400,
			"IpsecAuthAlg":"sha1",
			"IpsecPfs":"group2",
			"IpsecEncAlg":"aes"
		},
		"Local":"139.196.32.xx",
		"Remote":"116.62.69.64",
		"LocalSubnet":"2.2.2.0/24",
		"IkeConfig":{
			"IkeEncAlg":"aes",
			"RemoteId":"116.62.69.xx",
			"IkePfs":"group2",
			"IkeAuthAlg":"sha1",
			"Psk":"pgw6dy7d1i8i****",
			"IkeMode":"main",
			"IkeLifetime":86400,
			"IkeVersion":"ikev1",
			"LocalId":"139.196.32.xx"
		}
	}
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. Apply for the permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|404|InvalidVpnConnectionInstanceId.NotFound|The specified vpn connection instance id does not exist.|The error message returned because the specified IPsec-VPN connection does not exist. You must check whether the ID of the IPsec-VPN connection is valid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

