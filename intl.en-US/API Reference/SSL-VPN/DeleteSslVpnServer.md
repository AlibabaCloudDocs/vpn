# DeleteSslVpnServer

Deletes an SSL-VPN server.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DeleteSslVpnServer&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteSslVpnServer|The operation that you want to perform.

 Set the value to **DeleteSslVpnServer**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the SSL-VPN server is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|SslVpnServerId|String|Yes|vss-bp18q7hzj6largv4v\*\*\*\*|The ID of the SSL-VPN server. |
|ClientToken|String|No|02fb3da4-130e-11e9-8e44-0016e04115b|The client token that is used to guarantee the idempotence of the request.

 You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|606998F0-B94D-48FE-8316-ACA81BB230DA|The ID of the request. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=DeleteSslVpnServer
&RegionId=cn-hangzhou
&SslVpnServerId=vss-bp18q7hzj6largv4v****
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DeleteSslVpnServerResponse>
      <RequestId>606998F0-B94D-48FE-8316-ACA81BB230DA</RequestId>
</DeleteSslVpnServerResponse>
```

`JSON` format

```
{
	"RequestId":"606998F0-B94D-48FE-8316-ACA81BB230DA"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. You can apply for the permission and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|400|VpnGateway.Configuring|The specified service is configuring.|The error message returned because the specified service is being configured. Try again later.|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|The error message returned because the service is suspended due to overdue payments. Add funds before you enable the service.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

