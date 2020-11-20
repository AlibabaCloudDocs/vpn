# CreateSslVpnClientCert

Creates an SSL client certificate.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=CreateSslVpnClientCert&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateSslVpnClientCert|The operation that you want to perform.

 Set the value to **CreateSslVpnClientCert**. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region where the associated VPN gateway is created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|SslVpnServerId|String|Yes|vss-m5et0q3iy1qex328w\*\*\*\*|The ID of the SSL server. |
|ClientToken|String|No|02fb3da4-130e-11e9-8e44-0016e04115b|The client token that is used to guarantee the idempotence of the request.

 You can use the client to generate the value, but you must ensure that it is unique among different requests. The token can only contain ASCII characters and cannot exceed 64 characters in length. |
|Name|String|No|SslVpnClientCert1|The name of the SSL client certificate.

 The name must be 2 to 128 characters in length, and can contain digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter, and cannot start with `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Name|String|SslVpnClientCert|The name of the SSL client certificate. |
|RequestId|String|079874CD-AEC1-43E6-AC03-ADD96B6E4907|The ID of the request. |
|SslVpnClientCertId|String|vsc-m5euof6s5jy8vs5kd\*\*\*\*|The ID of the SSL client certificate. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=CreateSslVpnClientCert
&RegionId=cn-hangzhou
&SslVpnServerId=vss-m5et0q3iy1qex328w****
&<Common request parameters>

```

Sample success responses

`XML` format

```
<CreateSslVpnClientCertResponse>
      <SslVpnClientCertId>vsc-bp1n8wcf134yl0osr****</SslVpnClientCertId>
      <RequestId>606998F0-B94D-48FE-8316-ACA81BB230DA</RequestId>
</CreateSslVpnClientCertResponse>
```

`JSON` format

```
{
	"RequestId":"606998F0-B94D-48FE-8316-ACA81BB230DA",
	"SslVpnClientCertId":"vsc-bp1n8wcf134yl0osr****"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. Apply for the permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|
|400|Resource.QuotaFull|The quota of resource is full|The error message returned because the quota limit is reached.|
|400|VpnGateway.Configuring|The specified service is configuring.|The error message returned because the specified service is being configured. Try again later.|
|400|VpnGateway.FinancialLocked|The specified service is financial locked.|The error message returned because the service is suspended due to overdue payments. Top up your account first.|
|400|InvalidName|The name is not valid|The error message returned because the format of the specified name is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

