# TagResources

调用TagResources为指定的资源统一创建并绑定标签。

## API描述

标签是您为实例分配的标记，每个标签都由一对键值对（Key-Value）组成。标签的使用说明如下：

-   一个实例上的每条标签的标签键（Key）必须唯一。
-   不支持未绑定实例的空标签存在，标签必须绑定在实例上。
-   不同地域下的标签信息不互通。

    例如在华东1（杭州）地域创建的标签在华东2（上海）地域不可见。

-   同账号同地域下，专有网络、路由表、交换机和弹性公网IP的标签信息互通。

    例如在同账号同地域下，专有网络绑定了某个标签，那么您可以在交换机、路由表或弹性公网IP的编辑标签页面，直接选择将该标签绑定到实例上，而无需手动输入标签的键值信息。您可以修改标签的键和值，也可以随时删除实例的标签。如果删除实例，绑定实例的所有标签也会被删除。

-   单个实例最多可绑定20条标签。绑定标签前，阿里云会校验资源已有标签数量。超过限制值后返回报错信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=TagResources&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|TagResources|要执行的操作，取值：**TagResources**。 |
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
|Tag.N.Key|String|否|FinanceDept|资源的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持64个字符，必须以字母或中文开头，可包含数字、英文句点（.）、下划线（\_）和短划线（-），不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|否|FinanceJoshua|资源的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，必须以字母或中文开头，可包含数字、英文句点（.）、下划线（\_）和短划线（-），不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|请求ID。 |

## 示例

请求示例

```
http(s)://vpc.aliyuncs.com/?Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=vpc-bp16qjewdsunr41m1****
&ResourceType=VPC
&Tag.1.Key=FinanceDept
&Tag.1.Value=FinanceJoshua
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<TagResourcesResponse>
      <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</TagResourcesResponse>
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/Vpc)查看更多错误码。

