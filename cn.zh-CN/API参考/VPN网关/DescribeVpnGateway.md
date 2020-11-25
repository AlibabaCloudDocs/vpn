# DescribeVpnGateway

调用DescribeVpnGateway接口查询指定VPN网关的详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DescribeVpnGateway&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeVpnGateway|要执行的操作，取值：**DescribeVpnGateway**。 |
|RegionId|String|是|cn-shanghai|VPN网关所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpnGatewayId|String|是|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关的ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|DE77A7F3-3B74-41C0-A5BC-CAFD188C28B6|请求ID。 |
|VpnGatewayId|String|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关的ID。 |
|VpcId|String|vpc-bp1ub1yt9cvakoelj\*\*\*\*|VPN网关所属VPC的ID。 |
|VSwitchId|String|vsw-bp1y9ovl1cu9ou4tv\*\*\*\*|VPN网关所属交换机的ID。 |
|InternetIp|String|116.62.222.XX|公网IP地址。 |
|CreateTime|Long|1495382400000|VPN网关的创建时间。 |
|EndTime|Long|1495382400000|VPN网关的到期时间。 |
|Spec|String|5|VPN网关的规格。 |
|Name|String|vpngatewayname|VPN网关的名称。 |
|Description|String|vpngatewaydescription|VPN网关的描述信息。 |
|Status|String|init|VPN网关的状态。 |
|BusinessStatus|String|Normal|VPN网关的付费状态。 |
|ChargeType|String|PayByTraffic|付费类型。 |
|IpsecVpn|String|enable|是否开启了IPsec-VPN功能。 |
|SslVpn|String|enable|是否开启了SSL-VPN功能。 |
|SslMaxConnections|Long|5|最大SSL-VPN并发连接用户数的规格。 |
|Tag|String|tag1|VPN网关标签。 |

## 示例

请求示例

```
https://vpc.aliyuncs.com/?Action=DescribeVpnGateway
&RegionId=cn-shanghai
&VpnGatewayId=vpn-bp1q8bgx4xnkm2ogj****
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|指定的 VPN 网关不存在，请您检查 VPN 网关是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

