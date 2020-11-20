# CreateCustomerGateway

Creates a customer gateway.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=CreateCustomerGateway&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateCustomerGateway|The operation that you want to perform. Set the value to **CreateCustomerGateway**. |
|IpAddress|String|Yes|116.xx.xx.12|The public IP address of the VPN gateway in the on-premises data center. |
|RegionId|String|Yes|cn-shanghai|The region to which the customer gateway belongs.

 You can call the [DescribeRegions](~~36063~~) operation to query the region IDs. |
|ClientToken|String|No|02fb3da4-130e-11e9-8e44-0016e04115b|The client token that is used to guarantee the idempotence of the request.

 You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|Name|String|No|Gateway|The name of the customer gateway.

 The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). The name cannot start with `http://` or `https://`. |
|Description|String|No|Gateway|The description of the customer gateway.

 The description must be 2 to 256 characters in length. The description must start with a letter but cannot start with `http://` or `https://`. |
|Asn|String|No|10001|The autonomous system number of the on-premises data center. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CustomerGatewayId|String|cgw-bp1aw0a5nfff03xp1\*\*\*\*|The ID of the customer gateway. |
|IpAddress|String|101.xx.xx.12|The public IP address of the VPN gateway in the on-premises data center. |
|Name|String|test|The name of the customer gateway. |
|Description|String|test|The description of the customer gateway. |
|CreateTime|Long|1493363486000|The time when the customer gateway was created. |
|RequestId|String|D32B3C26-6C6C-4988-93E9-D2A6444CE6AE|The ID of the request. |

## Examples

Sample requests

```
https://vpc.aliyuncs.com/?Action=CreateCustomerGateway
&IpAddress=116.xx.xx.12
&RegionId=cn-shanghai
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateCustomerGatewayResponse>
      <CustomerGatewayId>cgw-bp1aw0a5nfff03xp****</CustomerGatewayId>
      <RequestId>185E81B1-3916-4667-B48F-C52409B33F2B</RequestId>
      <CreateTime>1493363486000</CreateTime>
      <IpAddress>101.xx.xx.12</IpAddress>
</CreateCustomerGatewayResponse>
```

`JSON` format

```
{
    "CustomerGatewayId": "cgw-bp1jrawp82av6bws9****",
    "CreateTime": 1493363599000,
    "RequestId": "D32B3C26-6C6C-4988-93E9-D2A6444CE6AE",
    "IpAddress": "101.xx.xx.12"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are not authorized to perform this operation on the specified resource. You can apply for the required permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are not authorized to perform this operation on the specified resource. To acquire the required permissions, submit a ticket.|
|400|InvalidIpAddress.AlreadyExist|Specified IpAddress is already exist.|The error message returned because this IP address already exists, The IP addresses must be unique in the same region.|
|400|InvalidIpAddress.WrongFormat|Specified IpAddress is invalid.|The error message returned because the specified IP address is invalid.|
|400|InvalidName|The name is not valid|The error message returned because the name format of the specified parameter is invalid.|
|400|InvalidDescription|The description is not valid|The error message returned because the description format of the specified parameter is invalid.|
|400|Resource.QuotaFull|The quota of resource is full|The error message returned because the resource has reached the quota limit.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

