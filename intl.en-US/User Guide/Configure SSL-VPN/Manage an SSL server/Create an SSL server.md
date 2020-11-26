# Create an SSL server

This topic describes how to create an SSL server. Before you use SSL-VPN to establish a site-to-site connection, you must create an SSL server.

A VPN gateway is created and SSL-VPN is enabled for the VPN gateway. For more information, see [Create a VPN gateway](/intl.en-US/User Guide/Manage a VPN Gateway/Create a VPN gateway.md).

1.  Log on to the [VPN gateway console](https://vpc.console.aliyun.com/vpn).

2.  In the left-side navigation pane, choose **VPN** \> **SSL Servers**.

3.  In the top navigation bar, select the region where you want to create the SSL server.

4.  On the **SSL Servers** page, click **Create SSL Server**.

5.  In the **Create SSL Server** dialog box, configure the SSL server based on the following information, and click **OK**.

    |Parameter|Description|
    |:--------|:----------|
    |**Name**|Enter a name for the SSL server. The name must be 2 to 128 characters in length, and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter. |
    |**VPN Gateway**|Select the VPN gateway that you want to associate with the SSL server. Make sure that SSL-VPN is enabled for the VPN gateway. |
    |**Local Network**|Enter the CIDR block of the network to be connected to the client through SSL-VPN. This value can be the CIDR block of a virtual private cloud \(VPC\), a VSwitch, an on-premises data center that is connected to a VPC through a leased line, or a cloud service such as ApsaraDB for RDS or Object Storage Service \(OSS\). Click **Add Local Network** to add more CIDR blocks.

**Note:** The subnet mask of the specified server CIDR block must be 8 to 32 bits in length. |
    |**Client Subnet**|Enter the CIDR block to be allocated to the virtual network interface of the client. Do not enter the CIDR block where the client resides. When the client accesses the server through an SSL-VPN connection, the VPN gateway selects an IP address from the specified CIDR block and assigns it to the client. **Note:** Make sure the server CIDR block and the client CIDR block do not overlap with each other. |
    |**Advanced Configuration**|
    |**Protocol**|Select the protocol over which the SSL-VPN connection is established. Supported protocols are UDP and TCP.|
    |**Port**|Specify the port to which the SSL-VPN connection is established. Default value: 1194.|
    |**Encryption Algorithm**|The encryption algorithm used by the SSL-VPN connection. Valid values: AES-128-CBC, AES-192-CBC, and AES-256-CBC.|
    |**Enable Compression**|Specify whether to enable data compression.|
    |**Two-factor Authentication**|Specify whether to enable two-factor authentication. You must select an IDaaS instance after you enable two-factor authentication. By default, you can use the username and password of IDaaS for two-factor authentication. You can also use Active Directory \(AD\) authentication. After you configure AD authentication, SSL-VPN is capable of using AD authentication to authenticate users.

**Note:**

    -   Only VPN gateways that are created after 00:00 \(UTC+8\), March 5, 2020 support two-factor authentication.
    -   If this is the first time you use two-factor authentication, you must authorize the VPN gateway to access the IDaaS instance before you create the SSL server. |


**Related topics**  


[CreateSslVpnServer](/intl.en-US/API reference/VPN Gateway/CreateSslVpnServer.md)

