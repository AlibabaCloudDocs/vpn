# DeleteSslVpnClientCert

调用DeleteSslVpnClientCert接口删除SSL-VPN客户端证书。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DeleteSslVpnClientCert&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteSslVpnClientCert|要执行的操作。

 取值： **DeleteSslVpnClientCert**。 |
|RegionId|String|是|cn-hangzhou|SSL-VPN客户端证书所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|SslVpnClientCertId|String|是|vsc-bp1n8wcf134yl0osr\*\*\*\*|SSL-VPN客户端证书的ID。 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-0016e04115b|

 客户端token，用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大不值过64个 ASCII 字符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|606998F0-B94D-48FE-8316-ACA81BB230DA|请求ID。 |

## 示例

请求示例

```

https://vpc.aliyuncs.com/?Action=DeleteSslVpnClientCert
&RegionId=cn-hangzhou
&SslVpnClientCertId=vsc-bp1n8wcf134yl0osr****
&<公共请求参数>

```

正常返回示例

`XML` 格式

```
<DeleteSslVpnClientCertResponse>
      <RequestId>606998F0-B94D-48FE-8316-ACA81BB230DA</RequestId>
</DeleteSslVpnClientCertResponse>
```

`JSON` 格式

```
{
	"RequestId":"606998F0-B94D-48FE-8316-ACA81BB230DA"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Vpc)查看更多错误码。

