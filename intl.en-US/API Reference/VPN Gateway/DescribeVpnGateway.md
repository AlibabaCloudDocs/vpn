# DescribeVpnGateway

Queries the details of a specified VPN gateway.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DescribeVpnGateway&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeVpnGateway|The operation that you want to perform. Set the value to **DescribeVpnGateway**. |
|RegionId|String|Yes|cn-shanghai|The region where the VPN gateway is deployed.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|VpnGatewayId|String|Yes|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the VPN gateway. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|DE77A7F3-3B74-41C0-A5BC-CAFD188C28B6|The ID of the request. |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the VPN gateway. |
|VpcId|String|vpc-bp1ub1yt9cvakoelj\*\*\*\*|The ID of the VPC to which the VPN gateway belongs. |
|VSwitchId|String|vsw-bp1y9ovl1cu9ou4tv\*\*\*\*|The ID of the VSwitch to which the VPN gateway is attached. |
|InternetIp|String|116.62.222.XX|The public IP address of the VPN gateway. |
|CreateTime|Long|1495382400000|The time when the VPN gateway was created. |
|EndTime|Long|1495382400000|The time when the VPN gateway expires. |
|Spec|String|5|The specification of the VPN gateway. |
|Name|String|vpngatewayname|The name of the VPN gateway. |
|Description|String|vpngatewaydescription|The description of the VPN gateway. |
|Status|String|init|The status of the VPN gateway. |
|BusinessStatus|String|Normal|The payment status of the VPN gateway. |
|ChargeType|String|PayByTraffic|The metering method of the VPN gateway. |
|IpsecVpn|String|enable|Indicates whether the IPsec-VPN feature is enabled. |
|SslVpn|String|enable|Indicates whether the SSL-VPN feature is enabled. |
|SslMaxConnections|Long|5|The maximum number of concurrent SSL-VPN connections. |
|Tag|String|tag1|The tag that is associated with the VPN gateway. |

## Examples

Sample requests

```
https://vpc.aliyuncs.com/?Action=DescribeVpnGateway
&RegionId=cn-shanghai
&VpnGatewayId=vpn-bp1q8bgx4xnkm2ogj****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeVpnGatewayResponse>
      <Status>active</Status>
      <VpnGatewayId>vpn-bp1q8bgx4xnkm2ogj****</VpnGatewayId>
      <Spec>5M</Spec>
      <BusinessStatus>Normal</BusinessStatus>
      <RequestId>98C99F30-A3D2-42E1-AC75-0C882FBE92F7</RequestId>
      <CreateTime>1492753580000</CreateTime>
      <InternetIp>116.62.69.xx</InternetIp>
      <EndTime>1495382400000</EndTime>
      <VSwitchId>vsw-bp1y9ovl1cu9ou4tv****</VSwitchId>
      <VpcId>vpc-bp1ub1yt9cvakoelj****</VpcId>
</DescribeVpnGatewayResponse>
```

`JSON` format

```
{
    "Status": "active",
    "VpnGatewayId": "vpn-bp1q8bgx4xnkm2ogj****",
    "BusinessStatus": "Normal",
    "Spec": "5M",
    "CreateTime": 1492753580000,
    "RequestId": "E98A9651-7098-40C7-8F85-C818D1EBBA85",
    "InternetIp": "116.62.69.xx",
    "EndTime": 1495382400000,
    "VSwitchId": "vsw-bp1y9ovl1cu9ou4tv****",
    "VpcId": "vpc-bp1ub1yt9cvakoelj****"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are not authorized to perform this operation on the specified resource. You can apply for the required permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are not authorized to perform this operation on the specified resource. To obtain the required permissions, submit a ticket.|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|The error message returned because the specified VPN connection does not exist. You can check whether the configuration of the VPN connection is valid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

