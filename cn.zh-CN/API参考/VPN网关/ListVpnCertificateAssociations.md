# ListVpnCertificateAssociations

调用ListVpnCertificateAssociations查询指定地域下VPN网关实例和证书的绑定关系。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Vpc&api=ListVpnCertificateAssociations&type=RPC&version=2016-04-28)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListVpnCertificateAssociations|系统规定参数。

 取值：**ListVpnCertificateAssociations**。 |
|RegionId|String|是|cn-hangzhou|地域ID。

 您可以通过调用[DescribeRegions](~~36063~~)接口获取地域ID。 |
|VpnGatewayId.N|RepeatList|否|vpn-bp1q8bgx4xnkm\*\*\*\*|VPN网关实例ID列表。 |
|CertificateId.N|RepeatList|否|6bfe4218-ea1d\*\*\*\*|证书ID列表。 |
|CertificateType|String|否|Encryption|证书类型。取值：

 -   **Encryption**：加密证书。
-   **Signature**：签名证书。 |
|NextToken|String|否|caeba0bbb2be0\*\*\*\*|查询凭证（Token）。

 取值为上一次调用API返回的**NextToken**参数值。如果没有下一个查询，请不传。 |
|MaxResults|Integer|否|10|分页大小，取值范围：**1**~**20**，默认为**10**。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|MaxResults|Integer|2|分页大小。 |
|NextToken|String|caeba0bbb2be\*\*\*\*|下一个查询开始Token。**NextToken**为空说明没有下一个。 |
|RequestId|String|197AF2BD-547F-470C-B29A-8400400233EB|请求ID。 |
|TotalCount|Integer|4|绑定关系总条目数。 |
|VpnCertificateRelations|Array of VpnCertificateRelation| |绑定关系列表。 |
|AssociationTime|String|2020-12-29T09:30:29Z|绑定时间。 |
|CertificateId|String|6bfe4218-ea1d\*\*\*\*|证书ID。 |
|CertificateType|String|Signature|证书类型。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|VpnGatewayId|String|vpn-bp1usbiorilk51760\*\*\*\*|VPN网关实例ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListVpnCertificateAssociations
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListVpnCertificateAssociationsResponse>
  <TotalCount>4</TotalCount>
  <RequestId>197AF2BD-547F-470C-B29A-8400400233EB</RequestId>
  <VpnCertificateRelations>
        <CertificateType>Signature</CertificateType>
        <AssociationTime>2020-12-29T09:30:29Z</AssociationTime>
        <VpnGatewayId>vpn-bp1usbiorilk51760****</VpnGatewayId>
        <CertificateId>6bfe4218-ea1d****</CertificateId>
        <RegionId>cn-hangzhou</RegionId>
  </VpnCertificateRelations>
  <VpnCertificateRelations>
        <CertificateType>Encryption</CertificateType>
        <AssociationTime>2020-12-29T09:30:16Z</AssociationTime>
        <VpnGatewayId>vpn-bp1usbiorilk51760****</VpnGatewayId>
        <CertificateId>6bfe4218-ea1d****</CertificateId>
        <RegionId>cn-hangzhou</RegionId>
  </VpnCertificateRelations>
  <VpnCertificateRelations>
        <CertificateType>Signature</CertificateType>
        <AssociationTime>2020-12-09T02:36:23Z</AssociationTime>
        <VpnGatewayId>vpn-bp1mrlw7134czer3l****</VpnGatewayId>
        <CertificateId>6bfe4218-ea1d****</CertificateId>
        <RegionId>cn-hangzhou</RegionId>
  </VpnCertificateRelations>
  <VpnCertificateRelations>
        <CertificateType>Encryption</CertificateType>
        <AssociationTime>2020-12-09T02:35:50Z</AssociationTime>
        <VpnGatewayId>vpn-bp1mrlw7134czer3l****</VpnGatewayId>
        <CertificateId>6bfe4218-ea1d****</CertificateId>
        <RegionId>cn-hangzhou</RegionId>
  </VpnCertificateRelations>
  <MaxResults>10</MaxResults>
</ListVpnCertificateAssociationsResponse>
```

`JSON`格式

```
{
  "TotalCount": 4,
  "RequestId": "197AF2BD-547F-470C-B29A-8400400233EB",
  "VpnCertificateRelations": [
    {
      "CertificateType": "Signature",
      "AssociationTime": "2020-12-29T09:30:29Z",
      "VpnGatewayId": "vpn-bp1usbiorilk51760****",
      "CertificateId": "6bfe4218-ea1d****",
      "RegionId": "cn-hangzhou"
    },
    {
      "CertificateType": "Encryption",
      "AssociationTime": "2020-12-29T09:30:16Z",
      "VpnGatewayId": "vpn-bp1usbiorilk51760****",
      "CertificateId": "6bfe4218-ea1d****",
      "RegionId": "cn-hangzhou"
    },
    {
      "CertificateType": "Signature",
      "AssociationTime": "2020-12-09T02:36:23Z",
      "VpnGatewayId": "vpn-bp1mrlw7134czer3l****",
      "CertificateId": "6bfe4218-ea1d****",
      "RegionId": "cn-hangzhou"
    },
    {
      "CertificateType": "Encryption",
      "AssociationTime": "2020-12-09T02:35:50Z",
      "VpnGatewayId": "vpn-bp1mrlw7134czer3l****",
      "CertificateId": "6bfe4218-ea1d****",
      "RegionId": "cn-hangzhou"
    }
  ],
  "MaxResults": 10
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden|User not authorized to operate on the specified resource.|您没有权限操作指定资源，请提交工单咨询。|

访问[错误中心](https://error-center.aliyun.com/status/product/Vpc)查看更多错误码。

