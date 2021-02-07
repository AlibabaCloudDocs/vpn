# AssociateVpnGatewayWithCertificate

调用AssociateVpnGatewayWithCertificate为VPN网关绑定证书。

## 背景信息

在您将VPN网关和证书进行绑定前，请先了解以下信息：

-   仅国密型VPN网关支持绑定证书。
-   首次绑定VPN网关和证书时，系统会自动创建一个名称为AliyunServiceRoleForVPNCertificate的服务关联角色，并且为该角色添加名称AliyunServiceRolePolicyForVPNCertificate的权限策略，授予VPN网关拥有访问其他云资源的权限。更多信息，请参见[AliyunServiceRoleForVPNCertificate](~~203323~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=AssociateVpnGatewayWithCertificate&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AssociateVpnGatewayWithCertificate|系统规定参数。

 取值：**AssociateVpnGatewayWithCertificate**。 |
|CertificateId|String|是|6bfe4218-ea1d\*\*\*\*|证书ID。 |
|CertificateType|String|是|Signature|证书类型。取值：

 -   **Encryption**：加密证书。
-   **Signature**：签名证书。 |
|RegionId|String|是|cn-hangzhou|VPN网关所在的地域ID。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpnGatewayId|String|是|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|VPN网关实例ID。

 **说明：** 仅国密型VPN网关支持绑定证书。 |
|ClientToken|String|否|0c593ea1-3bea\*\*\*\*|保证请求幂等性。

 从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。 |
|DryRun|Boolean|否|false|是否只预检此次请求。取值：

 -   **true**：表示只预检此次请求合法性，不会进行绑定操作。检查项包括是否填写了必需参数、请求格式、实例状态等。如果检查不通过，则返回对应错误；如果检查通过，则返回对应请求ID。
-   **false**（默认）：表示发送正常请求，通过检查后直接将VPN网关和证书进行绑定。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4EC47282-1B74-4534-BD0E-403F3EE64CAF|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=AssociateVpnGatewayWithCertificate
&CertificateId=6bfe4218-ea1d****
&CertificateType=Signature
&RegionId=cn-hangzhou
&VpnGatewayId=vpn-bp1q8bgx4xnkm2ogj****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<AssociateVpnGatewayWithCertificateResponse>
  <RequestId>4EC47282-1B74-4534-BD0E-403F3EE64CAF</RequestId>
</AssociateVpnGatewayWithCertificateResponse>
```

`JSON`格式

```
{
    "RequestId": "4EC47282-1B74-4534-BD0E-403F3EE64CAF"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|404|InvalidVpnGatewayInstanceId.NotFound|The specified vpn gateway instance id does not exist.|指定的 VPN 网关不存在，请您检查 VPN 网关是否正确。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

