# DeleteIpsecServer

调用DeleteIpsecServer删除IPsec服务端。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=DeleteIpsecServer&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteIpsecServer|系统规定参数。取值：**DeleteIpsecServer**。 |
|IpsecServerId|String|是|iss-bp1jougp8cfsbo8y9\*\*\*\*|IPsec服务端ID。 |
|RegionId|String|是|cn-hangzhou|IPsec服务端所属地域ID。 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-00\*\*\*\*|用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符。 |
|DryRun|String|否|false|是否只预检此次请求，取值：

 -   **true**：只预检此次请求，不会删除IPsec服务端。检查项包括是否填写了必需参数、请求格式、业务限制等。如果检查不通过，则返回对应错误信息。如果检查通过，则返回`DryRunOperation`。
-   **false**（默认值）：发送正常请求，通过检查后直接删除IPsec服务端。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0ED8D006-F706-4D23-88ED-E11ED28DCAC0|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeleteIpsecServer
&IpsecServerId=iss-bp1jougp8cfsbo8y9****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteIpsecServerResponse>
  <RequestId>0ED8D006-F706-4D23-88ED-E11ED28DCAC0</RequestId>
</DeleteIpsecServerResponse>
```

`JSON`格式

```
{
    "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28DCAC0"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

