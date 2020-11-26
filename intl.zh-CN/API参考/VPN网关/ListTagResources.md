# ListTagResources

调用ListTagResources查询云资源已经绑定的标签列表。

## API描述

-   请求中至少指定参数**ResourceId.N**或**Tag.N（Tag.N.Key与Tag.N.Value）**，以确定检索对象。
-   **Tag.N**是资源的标签，由一个键值对组成。仅指定**Tag.N.Key**时，则返回该标签键关联的所有标签值。仅指定**Tag.N.Value**会报错。
-   如果您同时指定**Tag.N**和**ResourceId.N**筛选标签，则**ResourceId.N**必须满足所有输入的标签键值对。
-   如果您同时指定多个标签键值对，返回结果为同时包含被指定的多个键值对的资源。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=ListTagResources&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTagResources|要执行的操作，取值：**ListTagResources**。 |
|RegionId|String|是|cn-hangzhou|资源所属的地域ID。 |
|ResourceType|String|是|VPC|资源类型，取值：

 -   **VPC**：专有网络实例。
-   **VSWITCH**：交换机实例。
-   **ROUTETABLE**：路由表实例。
-   **EIP**：弹性公网IP实例。
-   **VpnGateWay**：VPN网关实例。
-   **NATGATEWAY**：NAT网关实例。
-   **COMMONBANDWIDTHPACKAGE**：共享带宽实例。 |
|ResourceId.N|RepeatList|否|vpc-bp16qjewdsunr41m1\*\*\*\*|资源ID， N的取值范围为**1**~**20**。 |
|Tag.N.Key|String|否|FinanceDept|资源的标签键。N的取值范围：**1**~**20**。一旦传入该值，则不允许为空字符串。最多支持64个字符，必须以字母或中文开头，可包含数字、英文句点（.）、下划线（\_）和短划线（-），不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|否|FinanceJoshua|资源的标签值。N的取值范围：**1**~**20**。一旦传入该值，可以为空字符串。最多支持128个字符，必须以字母或中文开头，可包含数字、英文句点（.）、下划线（\_）和短划线（-），不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a4883|查询凭证（Token），取值为上一次API调用返回的NextToken参数值。如果没有下一个查询，请勿传参。 |
|MaxResults|Integer|否|50|分页大小，取值范围：**1**~**50**，默认为**50**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|下一个查询开始Token，NextToken为空说明没有下一个。 |
|RequestId|String|DE65F6B7-7566-4802-9007-96F2494AC512|请求ID。 |
|TagResources|Array of TagResource| |绑定标签的资源信息。 |
|TagResource| | | |
|ResourceId|String|vpc-bp16qjewdsunr41m1\*\*\*\*|资源ID。 |
|ResourceType|String|VPC|资源类型：

 -   **VPC**：专有网络实例。
-   **VSWITCH**：交换机实例。
-   **ROUTETABLE**：路由表实例。
-   **EIP**：弹性公网IP实例。
-   **VpnGateWay**：VPN网关实例。
-   **NATGATEWAY**：NAT网关实例。
-   **COMMONBANDWIDTHPACKAGE**：共享带宽实例。 |
|TagKey|String|FinanceDept|标签键。 |
|TagValue|String|FinanceJoshua|标签值。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=VPC
&ResourceId.1=vpc-bp16qjewdsunr41m1****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ListTagResourcesResponse>
  <TagResources>
        <TagResource>
              <ResourceType>VPC</ResourceType>
              <TagValue>aa</TagValue>
              <TagKey>aaa</TagKey>
              <ResourcId>vpc-wz9aml8mptq6fsnfm****</ResourcId>
        </TagResource>
  </TagResources>
  <NextToken></NextToken>
  <RequestId>F11AC96F-B8E6-48F8-95CC-F63E7D50F0D4</RequestId>
</ListTagResourcesResponse>
```

`JSON` 格式

```
{
	"TagResources": {
		"TagResource": [
			{
				"ResourceType": "VPC",
				"TagValue": "aa",
				"TagKey": "aaa",
				"ResourcId": "vpc-wz9aml8mptq6fsnfm****"
			}
		]
	},
	"NextToken": "",
	"RequestId": "F11AC96F-B8E6-48F8-95CC-F63E7D50F0D4"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Vpc)查看更多错误码。

