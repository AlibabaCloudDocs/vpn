# DescribeSslVpnServers

调用DescribeSslVpnServers接口查询已创建的SSL-VPN服务端。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DescribeSslVpnServers&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSslVpnServers|要执行的操作。

 取值： **DescribeSslVpnServers**。 |
|RegionId|String|是|cn-hangzhou|SSL-VPN服务端所在的地域ID。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|SslVpnServerId|String|否|vss-bp15j3du13gq1dgey\*\*\*\*|SSL-VPN服务端的ID。 |
|VpnGatewayId|String|否|vpn-bp1on0xae9d771ggi\*\*\*\*|VPN网关的ID。 |
|Name|String|否|test|SSL-VPN服务端的名称。 |
|PageNumber|Integer|否|1|列表的页码，默认值为**1**。 |
|PageSize|Integer|否|10|分页查询时每页的行数，最大值为**50**，默认值为**10**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|10|每页包含多少条目。 |
|RequestId|String|D350187B-EA41-4577-950B-95434C8302E1|请求ID。 |
|SslVpnServers|Array of SslVpnServer| |SSL-VPN服务端的详细信息。 |
|SslVpnServer| | | |
|Cipher|String|AES-128-CBC|使用的加密算法。 |
|ClientIpPool|String|10.10.1.0/24|客户端网段。 |
|Compress|Boolean|false|是否对通信进行压缩。 |
|Connections|Integer|0|当前连接数。 |
|CreateTime|Long|1613800884000|创建SSL-VPN服务端的时间戳。 |
|EnableMultiFactorAuth|Boolean|true|是否开启了双因子认证。

 -   **true**：已开启。
-   **false**（默认值）：未开启。 |
|IDaaSInstanceId|String|idaas-cn-hangzhou-\*\*\*\*|IDaaS实例ID。 |
|IDaaSRegionId|String|cn-hangzhou|IDaaS实例所属地域ID。 |
|InternetIp|String|47.XX.XX.5|VPN网关的公网IP地址。 |
|LocalSubnet|String|192.168.0.0/24|本端网段。 |
|MaxConnections|Integer|5|最大连接数。 |
|Name|String|test|SSL-VPN服务端名称。 |
|Port|Integer|1194|SSL-VPN服务端所使用的端口。 |
|Proto|String|UDP|SSL-VPN服务端所使用的协议。 |
|RegionId|String|cn-hangzhou|SSL-VPN服务端的地域ID。 |
|SslVpnServerId|String|vss-bp15j3du13gq1dgey\*\*\*\*|SSL-VPN服务端的ID。 |
|VpnGatewayId|String|vpn-bp1on0xae9d771ggi\*\*\*\*|VPN网关ID。 |
|TotalCount|Integer|1|列表条条目数。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeSslVpnServers
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeSslVpnServersResponse>
  <TotalCount>1</TotalCount>
  <RequestId>D350187B-EA41-4577-950B-95434C8302E1</RequestId>
  <PageSize>10</PageSize>
  <PageNumber>1</PageNumber>
  <SslVpnServers>
        <SslVpnServer>
              <LocalSubnet>10.10.1.0/24</LocalSubnet>
              <Compress>true</Compress>
              <Connections>0</Connections>
              <ClientIpPool>192.168.0.0/24</ClientIpPool>
              <IDaaSInstanceId>idaas-cn-hangzhou-p****</IDaaSInstanceId>
              <MaxConnections>5</MaxConnections>
              <EnableMultiFactorAuth>true</EnableMultiFactorAuth>
              <SslVpnServerId>vss-bp1phv0j000c78l3k****</SslVpnServerId>
              <CreateTime>1613800884000</CreateTime>
              <Port>1194</Port>
              <IDaaSRegionId>cn-hangzhou</IDaaSRegionId>
              <Name>test</Name>
              <Proto>TCP</Proto>
              <InternetIp>47.XX.XX.5</InternetIp>
              <VpnGatewayId>vpn-bp17lofy9fd0dnvzv****</VpnGatewayId>
              <RegionId>cn-hangzhou</RegionId>
              <Cipher>AES-128-CBC</Cipher>
        </SslVpnServer>
  </SslVpnServers>
</DescribeSslVpnServersResponse>
```

`JSON`格式

```
{
  "TotalCount": 1,
  "RequestId": "D350187B-EA41-4577-950B-95434C8302E1",
  "PageSize": 10,
  "PageNumber": 1,
  "SslVpnServers": {
    "SslVpnServer": [
      {
        "LocalSubnet": "10.10.1.0/24",
        "Compress": true,
        "Connections": 0,
        "ClientIpPool": "192.168.0.0/24",
        "IDaaSInstanceId": "idaas-cn-hangzhou-p****",
        "MaxConnections": 5,
        "EnableMultiFactorAuth": true,
        "SslVpnServerId": "vss-bp1phv0j000c78l3k****",
        "CreateTime": 1613800884000,
        "Port": 1194,
        "IDaaSRegionId": "cn-hangzhou",
        "Name": "test",
        "Proto": "TCP",
        "InternetIp": "47.XX.XX.5",
        "VpnGatewayId": "vpn-bp17lofy9fd0dnvzv****",
        "RegionId": "cn-hangzhou",
        "Cipher": "AES-128-CBC"
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

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

