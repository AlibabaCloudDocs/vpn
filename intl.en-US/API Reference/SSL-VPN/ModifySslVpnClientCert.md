# ModifySslVpnClientCert

Modifies the name of an SSL-VPN client certificate.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=ModifySslVpnClientCert&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySslVpnClientCert|The operation that you want to perform.

 Set the value to **ModifySslVpnClientCert**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the SSL-VPN client certificate is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|SslVpnClientCertId|String|Yes|vsc-bp1n8wcf134yl0osrc\*\*\*\*|The ID of the SSL-VPN client certificate. |
|ClientToken|String|No|02fb3da4-130e-11e9-8e44-0016e04115b|The client token that is used to guarantee the idempotence of the request.

 You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|Name|String|No|cert2|The name of the SSL-VPN client certificate.

 The name must be 2 to 128 characters in length, and can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot start with `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Name|String|cert2|The name of the SSL-VPN client certificate. |
|RequestId|String|606998F0-B94D-48FE-8316-ACA81BB230DA|The ID of the request. |
|SslVpnClientCertId|String|vsc-bp1n8wcf134yl0osr\*\*\*\*|The ID of the SSL-VPN client certificate. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=ModifySslVpnClientCert
&RegionId=cn-hangzhou
&SslVpnClientCertId=vsc-bp1n8wcf134yl0osr****
&Name=cert2
&<Common request parameters>

```

Sample success responses

`XML` format

```
<ModifySslVpnClientCertResponse>
      <SslVpnClientCertId>vsc-bp1n8wcf134yl0osr****</SslVpnClientCertId>
      <Name>cert2</Name>
      <RequestId>606998F0-B94D-48FE-8316-ACA81BB230DA</RequestId>
</ModifySslVpnClientCertResponse>
```

`JSON` format

```
{
	"Name":"cert2",
	"RequestId":"606998F0-B94D-48FE-8316-ACA81BB230DA",
	"SslVpnClientCertId":"vsc-bp1n8wcf134yl0osr****"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. You can apply for the permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|400|InvalidName|The name is not valid|The error message returned because the format of the specified name parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

