# UnTagResources

调用UntagResources为指定的资源列表统一解绑标签。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=UnTagResources&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UnTagResources|要执行的操作，取值：**UntagResources**。 |
|RegionId|String|是|cn-hangzhou|资源所属的地域ID。 |
|ResourceId.N|RepeatList|是|vpc-bp16qjewdsunr41m1\*\*\*\*|资源ID，N的取值范围为**1**~**20**。 |
|ResourceType|String|是|VPC|资源类型，取值：

 -   **VPC**：专有网络实例。
-   **VSWITCH**：交换机实例。
-   **ROUTETABLE**：路由表实例。
-   **EIP**：弹性公网IP实例。
-   **VpnGateWay**：VPN网关实例。
-   **NATGATEWAY**：NAT网关实例。
-   **COMMONBANDWIDTHPACKAGE**：共享带宽实例。 |
|TagKey.N|RepeatList|否|FinanceDept|要解绑的标签键。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持64个字符，必须以字母或中文开头，可包含数字、英文句点（.）、下划线（\_）和短划线（-），不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UnTagResources
&RegionId=cn-hangzhou	
&ResourceId.1=vpc-bp16qjewdsunr41m1****
&ResourceType=VPC
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UntagResourcesResponse>
      <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</UntagResourcesResponse>
```

`JSON` 格式

```
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

