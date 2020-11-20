# Make API calls

VPN Gateway and Virtual Private Cloud \(VPC\) use the same API endpoint. You can send HTTP GET requests to call the VPN Gateway API. You must add the request parameters that correspond to the API operation being called. After you call the API operation, the system returns a response. The request and response are encoded in UTF-8.

## Request syntax

VPN Gateway API operations use the Remote Procedure Call \(RPC\) protocol. You can call VPN Gateway API operations by sending HTTP GET requests.

The request syntax is:

```
http://Endpoint/?Action=xx&Parameters
```

where:

-   Endpoint: the endpoint of the VPN Gateway API. The endpoint is `vpc.aliyuncs.com`.
-   Action: the name of the operation that you want to perform. For example, to create a VPN gateway, you must set the Action parameter to CreateVpnGateway.
-   Version: the version number of the VPN Gateway API that you want to call. The version of VPN Gateway API is 2016-04-28.
-   Parameters: the request parameters for the operation. Separate multiple parameters with ampersands \(&\).

    Request parameters include common parameters and operation-specific parameters. Common parameters include information such as the API version number and authentication information. For more information, see [Common parameters](/intl.en-US/API reference/HTTP Requests/Common parameters.md).


The following example demonstrates how to call the CreateVpnGateway operation to create a VPN gateway:

**Note:** The following code has been edited to improve readability.

```
https://vpc.aliyuncs.com/?Action=CreateVpnGateway
&Format=xml
&Version=2016-04-28
&Signature=xxxx%xxxx%3D
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&AccessKeyId=key-test
&Timestamp=2012-06-01T12:00:00Z
…
```

## Authorization

To ensure the security of your account, we recommend that you call the VPN Gateway API as a RAM user. Before you call the VPN Gateway API as a RAM user, you must create a RAM user and grant the RAM user the required permissions.

For more information about VPN gateway resources and API operations that you can authorize a RAM user to use, see [RAM user authorization](/intl.en-US/API reference/RAM user authorization.md).

## Signature

You must sign all API requests to ensure security. Alibaba Cloud uses the request signature to verify the identity of the API caller.

VPN Gateway implements symmetric encryption with an AccessKey pair to verify the identity of a request sender. An AccessKey pair is an identity credential issued to Alibaba Cloud accounts and RAM users. An AccessKey pair is similar to a pair of username and password. An AccessKey pair consists of an AccessKey ID and an AccessKey secret. The AccessKey ID is used to verify the identity of the user, while the AccessKey secret is used to encrypt and verify the signature string. You must keep your AccessKey secret strictly confidential.

To call an RPC API operation, you must add the signature to the API request in the following format:

`https://endpoint/?SignatureVersion=1.0&SignatureMethod=HMAC-SHA1&Signature=XXXX%3D&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0axxxxxxxx`

Take CreateVpnGateway as an example. Assume that the AccessKey ID is `testid` and the AccessKey secret is `testsecret`, the following code shows the request URL before the request is signed:

```
http://vpc.aliyuncs.com/?Action=CreateVpnGateway
&Timestamp=2016-05-23T12:46:24Z
&Format=XML
&AccessKeyId=testid
&SignatureMethod=HMAC-SHA1
&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0axxxxxxxx
&Version=2014-05-26
&SignatureVersion=1.0
```

Perform the following steps to calculate the signature:

1.  Use the request parameters to create a string-to-sign.

    ```
    GET&%2F&AccessKeyId%3Dtestid&Action%3DCreateVpnGateway&Format%3DXML&SignatureMethod%3DHMAC-SHA1&SignatureNonce%3D3ee8c1b8-83d3-44af-a94f-4e0axxxxxxxx&SignatureVersion%3D1.0&TimeStamp%3D2016-02-23T12%253A46%253A24Z&Version%3D2014-05-15
    ```

    .

2.  Calculate the HMAC value of the string-to-sign.

    Append an ampersand \(&\) to the AccessKey secret as the key to calculate the HMAC value. In this example, the key is `testsecret&`.

    ```
    CT9X0VtwR86fNWS********juE=
    ```

3.  Add the signature string to the request:

    ```
    http://vpc.aliyuncs.com/?Action=CreateVpnGateway
    &Timestamp=2016-05-23T12:46:24Z
    &Format=XML
    &AccessKeyId=testid
    &SignatureMethod=HMAC-SHA1
    &SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0axxxxxxxx
    &Version=2014-05-26
    &SignatureVersion=1.0
    &Signature=XXXX%3D
    ```


