# DescribeCustomerGateways

Queries customer gateways.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Vpc&api=DescribeCustomerGateways&type=RPC&version=2016-04-28)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCustomerGateways|The operation that you want to perform.

 Set the value to **DescribeCustomerGateways**. |
|RegionId|String|Yes|cn-shanghai|The ID of the region where the customer gateways are created.

 You can call the [DescribeRegions](~~36063~~) operation to query region IDs. |
|CustomerGatewayId|String|No|vpn-bp1q8bgx4xnkm2ogj\*\*\*\*|The ID of the customer gateway. |
|PageNumber|Integer|No|1|The number of the page to return. Default value: **1**. |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: **50**. Default value: **10**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CustomerGateways| | |Detailed information about the customer gateway. |
|CustomerGatewayId|String|cgw-bp1pvpl9r9adju6l5\*\*\*\*|The ID of the customer gateway. |
|Name|String|test|The name of the customer gateway. |
|Description|String|test|The description of the customer gateway. |
|IpAddress|String|139.196.32.xxx|The IP address of the customer gateway. |
|CreateTime|Long|1492747187000|The time when the customer gateway was created. |
|TotalCount|Integer|1|The number of entries returned. |
|PageNumber|Integer|1|The number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|5BE01CD7-5A50-472D-AC14-CA181C5C03BE|The ID of the request. |

## Examples

Sample requests

```

https://vpc.aliyuncs.com/?Action=DescribeCustomerGateways
&RegionId=cn-shanghai
&<Common request parameters>

```

Sample success responses

`XML` format

```
<DescribeCustomerGatewaysResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>5BE01CD7-5A50-472D-AC14-CA181C5C03BE</RequestId>
      <CustomerGateways>
            <CustomerGateway>
                  <Name>test</Name>
                  <CustomerGatewayId>cgw-bp1pvpl9r9adju6l5****</CustomerGatewayId>
                  <CreateTime>1492747187000</CreateTime>
                  <IpAddress>139.196.32.xxx</IpAddress>
            </CustomerGateway>
      </CustomerGateways>
</DescribeCustomerGatewaysResponse>
```

`JSON` format

```
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"E82612A9-CB90-4D7E-B394-1DB7F6509B29",
	"CustomerGateways":{
		"CustomerGateway":[
			{
				"CustomerGatewayId":"cgw-bp1pvpl9r9adju6l5****",
				"Name":"test",
				"CreateTime":1492747187000,
				"IpAddress":"139.196.32.xxx"
			}
		]
	}
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbbiden.SubUser|User not authorized to operate on the specified resource as your account is created by another user.|The error message returned because you are unauthorized to perform the operation on the specified resource. Apply for the permissions and try again.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned because you are unauthorized to perform the operation on the specified resource. To acquire the required permissions, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Vpc).

