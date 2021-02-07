# DissociateVpnGatewayWithCertificate

调用DissociateVpnGatewayWithCertificate解除VPN网关和证书的绑定关系。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DissociateVpnGatewayWithCertificate&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DissociateVpnGatewayWithCertificate|系统规定参数。

 取值：**DissociateVpnGatewayWithCertificate**。 |
|CertificateId|String|是|6bfe4218-ea1d\*\*\*\*|证书ID。 |
|CertificateType|String|是|Encryption|证书类型。取值：

 -   **Encryption**：加密证书。
-   **Signature**：签名证书。 |
|RegionId|String|是|cn-hangzhou|VPN网关所在的地域ID。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpnGatewayId|String|是|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关实例ID。 |
|ClientToken|String|否|02fb3da4-130e\*\*\*\*\*\*\*|用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符。 |
|DryRun|Boolean|否|false|是否只预检此次请求。取值：

 -   **true**：表示只预检此次请求合法性，不会进行解绑操作。检查项包括是否填写了必需参数、请求格式、实例状态等。如果检查不通过，则返回对应错误；如果检查通过，则返回对应请求ID。
-   **false**（默认）：表示发送正常请求，通过检查后直接对VPN网关和证书进行解绑。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|611CB80C-B6A9-43DB-9E38-0B0AC3D9B58F|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DissociateVpnGatewayWithCertificate
&CertificateId=6bfe4218-ea1d****
&CertificateType=Encryption
&RegionId=cn-hangzhou
&VpnGatewayId=vpn-bp1q8bgx4xnkm2ogj****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DissociateVpnGatewayWithCertificateResponse>  
  <RequestId>611CB80C-B6A9-43DB-9E38-0B0AC3D9B58F</RequestId>
</DissociateVpnGatewayWithCertificateResponse>
```

`JSON`格式

```
{
    "RequestId": "611CB80C-B6A9-43DB-9E38-0B0AC3D9B58F"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|指定的 VPN 网关不存在，请您检查 VPN 网关是否正确。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

