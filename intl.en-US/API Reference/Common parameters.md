# Common parameters

Common parameters include common request parameters and common response parameters.

## Common request parameters

Common request parameters must be included in all VPC API requests. The following table lists the common request parameters.

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Format|String|No|The format in which the response is returned. Valid value: JSON and XML. Default value: JSON. |
|Version|String|Required|The version number of the API. Format: `YYYY-MM-DD`. Set the value to 2016-04-28 |
|AccessKeyId|String|Required|The AccessKey ID provided to you by Alibaba Cloud.|
|Signature|String|Required|The signature string of the current request.|
|SignatureMethod|String|Required|The encryption method of the signature string. Set the value to HMAC-SHA1 |
|Timestamp|String|Required|The timestamp of the request. Specify the time in the ISO 8601 standard in the `YYYY-MM-DDThh:mm:ssZ` format. The time must be in UTC. For example, you can set this parameter to 2013-01-10T12:00:00Z, which indicates 20:00:00 on January 10, 2013 \(UTC+8\). |
|SignatureVersion|String|Required|The version of the signature encryption algorithm. Set the value to 1.0 |
|SignatureNonce|String|Required|A unique, random number used to prevent replay attacks. You must use different numbers for different requests. |

## Common response parameters

API responses use the HTTP response format where a 2xx status code indicates a successful call and a 4xx or 5xx status code indicates a failed call. Responses can be returned in the JSON or XML format. The default response format is JSON. You can specify the response format when you call an operation.

Every response returns a unique RequestId regardless of whether the call is successful.

-   XML format

    ```
    <? xml version="1.0" encoding="utf-8"? > 
        <!—Result root node-->
        <Operation name+Response>
            <!—Returned request tag-->
            <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
            <!—Returned data-->
        </Operation name+Response>
                        
    ```

-   JSON format

    ```
    {
        "RequestId":"4C467B38-3910-447D-87BC-AC049166F216",
        /*Returned data*/
        }
    ```


