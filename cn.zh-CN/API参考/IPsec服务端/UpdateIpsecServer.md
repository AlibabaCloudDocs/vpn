# UpdateIpsecServer

调用UpdateIpsecServer更新IPsec服务端配置。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=UpdateIpsecServer&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateIpsecServer|系统规定参数。取值：**UpdateIpsecServer**。 |
|IpsecServerId|String|是|iss-bp1bo3xuvcxo7ixll\*\*\*\*|IPsec服务端ID。 |
|RegionId|String|是|cn-shanghai|IPsec服务端所属地域ID。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|LocalSubnet|String|否|192.XX.XX.0/24,10.XX.XX.0/24|本端网段，指需要和客户端网段互连的VPC侧的网段。

 多个网段之间用半角逗号（,）分隔，例如：192.168.1.0/24,192.168.2.0/24。 |
|ClientIpPool|String|否|10.XX.XX.0/24|客户端网段，指给客户端虚拟网卡分配访问地址的网段。 |
|IpsecServerName|String|否|test|IPsec服务端名称。

 名称长度为2~128个字符，以英文字母或中文开始，可包含数字、短划线（-）和下划线（\_）。 |
|EffectImmediately|Boolean|否|false|是否删除当前已协商成功的IPsec隧道并重新发起协商。取值：

 -   **true**：配置完成后立即进行协商。
-   **false**（默认值）：当有流量进入时进行协商。 |
|IkeConfig|String|否|\{"IkeVersion":"ikev2","IkeMode":"main","IkeEncAlg":"aes","IkeAuthAlg":"sha1","IkePfs":"group2","IkeLifetime":86400\}|第一阶段协商参数配置。

 -   **IkeVersion**：IKE协议的版本。取值：**ikev1**或**ikev2**，默认值：**ikev2**。
-   **IkeMode**：IKE版本的协商模式。默认值：**main**。
-   **IkeEncAlg**：第一阶段协商的加密算法。默认值：**aes**。
-   **IkeAuthAlg**：第一阶段协商的认证算法。默认值：**sha1**。
-   **IkePfs**：第一阶段协商使用的Diffie-Hellman密钥交换算法。默认值：**group2**。
-   **IkeLifetime**：第一阶段协商出的SA的生存周期。默认值：**86400**，单位为秒。
-   **LocalId**：IPsec服务端标识。支持FQDN和IP地址格式，默认值为VPN网关公网IP地址。
-   **RemoteId**：对端标识。支持FQDN和IP地址格式，默认值为空。 |
|IpsecConfig|String|否|\{"IpsecEncAlg":"aes","IpsecAuthAlg":"sha1","IpsecPfs":"group2","IpsecLifetime":86400\}|第二阶段协商参数配置。

 -   **IpsecEncAlg**：第二阶段协商的加密算法。默认值：**aes**。
-   **IpsecAuthAlg**：第二阶段协商的认证算法。默认值：**sha1**。
-   **IpsecPfs**：转发所有协议的报文。第二阶段协商使用的Diffie-Hellman密钥交换算法。默认值：**group2**。
-   **IpsecLifetime**：第二阶段协商出的SA的生存周期。默认值：**86400**，单位为秒。 |
|PskEnabled|Boolean|否|true|是否开启预共享密钥认证方式。仅取值为**true**，表示开启预共享密钥认证方式。 |
|Psk|String|否|123456|预共享密钥。

 用于VPN网关与客户端之间的身份认证。默认情况下会随机生成一个16位的随机字符串，也可以手动指定密钥。长度限制为100个字符。 |
|ClientToken|String|否|e4567-e89b-12d3-a456-42665544\*\*\*\*|保证请求幂等性。

 从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。 |
|DryRun|String|否|false|是否只预检此次请求，取值：

 -   **true**：只预检此次请求，不会更改IPsec服务端配置。检查项包括是否填写了必需参数、请求格式、业务限制等。如果检查不通过，则返回对应错误信息。如果检查通过，则返回`DryRunOperation`。
-   **false**（默认值）：发送正常请求，通过检查后直接更改IPsec服务端配置。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B61C08E5-403A-46A2-96C1-F7B1216DB10C|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UpdateIpsecServer
&IpsecServerId=iss-bp1bo3xuvcxo7ixll****
&RegionId=cn-shanghai
&<公共请求参数>
```

正常返回示例

`XML`格式

```
</UpdateIpsecServerResponse>
<RequestId>B61C08E5-403A-46A2-96C1-F7B1216DB10C</RequestId>
</UpdateIpsecServerResponse>
```

`JSON`格式

```
{
    "RequestId": "B61C08E5-403A-46A2-96C1-F7B1216DB10C"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|
|400|VpnGateway.Configuring|The specified service is configuring.|服务正在配置中，请您稍后再试。|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|该服务已欠费，请您先充值再操作。|
|400|IllegalParam.LocalSubnet|The specified "LocalSubnet" \(%s\) is invalid.|本端网段\(%s\)不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

