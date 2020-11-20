# CreateCustomerGateway

调用CreateCustomerGateway接口创建用户网关。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=CreateCustomerGateway&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateCustomerGateway|要执行的操作。取值：**CreateCustomerGateway**。 |
|IpAddress|String|是|116.xx.xx.12|本地数据中心VPN网关的公网IP地址。 |
|RegionId|String|是|cn-shanghai|用户网关所在的地域。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|ClientToken|String|否|02fb3da4-130e-11e9-8e44-0016e04115b|客户端token，用于保证请求的幂等性。

 由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符。 |
|Name|String|否|Gateway|用户网关的名称。

 长度为2~128个字符，必须以字母或中文开头，可包含数字、点号（.）、下划线（\_）和短横线（-）。但不能以`http://`或`https://`开头。 |
|Description|String|否|Gateway|用户网关的描述信息。

 长度为2~256个字符，必须以字母或中文开头，但不能以`http://`或`https://`开头。 |
|Asn|String|否|10001|本地数据中心的自治系统号。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|CustomerGatewayId|String|cgw-bp1aw0a5nfff03xp1\*\*\*\*|用户网关的ID。 |
|IpAddress|String|101.xx.xx.12|本地数据中心VPN网关的公网IP地址。 |
|Name|String|test|用户网关的名称。 |
|Description|String|test|用户网关的描述信息。 |
|CreateTime|Long|1493363486000|用户网关的创建时间。 |
|RequestId|String|D32B3C26-6C6C-4988-93E9-D2A6444CE6AE|请求ID。 |

## 示例

请求示例

```
https://vpc.aliyuncs.com/?Action=CreateCustomerGateway
&IpAddress=116.xx.xx.12
&RegionId=cn-shanghai
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateCustomerGatewayResponse>
      <CustomerGatewayId>cgw-bp1aw0a5nfff03xp****</CustomerGatewayId>
      <RequestId>185E81B1-3916-4667-B48F-C52409B33F2B</RequestId>
      <CreateTime>1493363486000</CreateTime>
      <IpAddress>101.xx.xx.12</IpAddress>
</CreateCustomerGatewayResponse>
```

`JSON` 格式

```
{
    "CustomerGatewayId": "cgw-bp1jrawp82av6bws9****",
    "CreateTime": 1493363599000,
    "RequestId": "D32B3C26-6C6C-4988-93E9-D2A6444CE6AE",
    "IpAddress": "101.xx.xx.12"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|您没有权限操作该资源，请您申请操作权限后再试。|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|InvalidIpAddress.AlreadyExist|Specified IpAddress is already exist.|该IP已经存在，原因是同一个用户在同一个region内，IP不可重复。|
|400|InvalidIpAddress.WrongFormat|Specified IpAddress is invalid.|该IP不合法。|
|400|InvalidName|The name is not valid|该名称格式不合法。|
|400|InvalidDescription|The description is not valid|描述格式不合法。|
|400|Resource.QuotaFull|The quota of resource is full|资源配额已达上限。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Vpc)查看更多错误码。

