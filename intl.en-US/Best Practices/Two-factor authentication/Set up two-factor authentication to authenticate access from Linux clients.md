# Set up two-factor authentication to authenticate access from Linux clients

This topic describes how to set up two-factor authentication to authenticate access from Linux clients to Virtual Private Cloud \(VPC\).

Prerequisites

-   An Identity as a Service \(IDaaS\) instance is purchased and the user information of the IDaaS instance is updated on Alibaba Cloud. For more information, see [Organizations]() and [Accounts]().
-   A VPC network is created. For more information, see [Create a VPC](/intl.en-US/VPCs and VSwitches/VPC management/Create a VPC.md).

In this example, a company has created a VPC network in the China \(Hangzhou\) region and the CIDR block is 192.168.1.0/24. Due to service requirements, a staff member needs to access the VPC network from a Linux client.

![Two-factor authentication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0927325951/p88538.png)

As shown in the preceding figure, you can create a VPN Gateway instance on Alibaba Cloud, configure the SSL Certificates Service server, and then enable two-factor authentication. To access resources deployed in an SSL-VPN enabled VPC network, you must pass both SSL authentication and two-factor authentication. This improves the security and manageability of VPN connections.

## Procedure

![Two-factor authentication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0927325951/p88539.png)

## Step 1: Create a VPN Gateway instance

VPN Gateway is an Internet-based service that securely and reliably connects enterprise data centers, office networks, or Internet-facing terminals to Alibaba Cloud VPC networks through encrypted connections.

**Note:** Make sure that the VPN Gateway instance was created after 00:00, March 5, 2020. Otherwise, two-factor authentication is not supported.

1.  Log on to the [VPN gateway console](https://vpc.console.aliyun.com/vpn).

2.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.

3.  On the **VPN Gateways** page, click **Create VPN Gateway**.

4.  On the buy page, set the following parameters and click **Buy Now** to complete the payment:

    -   **Name**: Enter a name for the VPN Gateway instance.
    -   **Region**: Select the region where the instance will be deployed. In this example, select **China \(Hangzhou\)**.

        **Note:** The VPC network that you want to connect and the VPN Gateway instance must be located in the same region.

    -   **VPC**: Select the VPC network that you want to connect.
    -   **Peak Bandwidth**: Select the maximum bandwidth of the VPN Gateway instance. This value is the upper limit of public network bandwidth supported by the VPN Gateway instance. In this example, select **5Mbps**.
    -   **IPsec-VPN**: Enable or disable the IPsec-VPN feature. After you enable this feature, you can establish connections between an on-premises data center and a VPC network or between two VPC networks. In this example, select **Disable**.
    -   **SSL-VPN**: You can enable or disable SSL-VPN feature. After you enable this feature, you can connect to the VPC network from a client in any region. In this example, select **Enable**.
    -   **SSL connections**: Select the maximum number of concurrent SSL Certificates Service connections. In this example, select **5**.

        **Note:** You can configure SSL Certificates Service connections only when SSL-VPN authentication is enabled.

    -   **Billing Cycle**: Select a billing cycle for the VPN Gateway instance.

## Step 2: Create an SSL Certificates Service server

SSL-VPN is based on the OpenVPN framework. You must use an SSL Certificates Service server to specify the CIDR blocks that you want to connect to and the CIDR blocks that the client uses, and enable two-factor authentication.

1.  In the left-side navigation pane, click **VPN** \> **SSL Servers**.

2.  In the top navigation bar, select the region of the SSL Certificates Service server.

    In this example, select **China \(Hangzhou\)**.

3.  On the **SSL Servers** page, click **Create SSL Server**.

4.  On the **Create SSL Server** page, set the following parameters and click **OK**:

    -   **Name**: Enter a name for the SSL Certificates Service server.
    -   **VPN Gateway**: Select the VPN Gateway instance that is specified in step 1.
    -   **Local Network**: Enter the CIDR blocks used in the connections by the client through SSL-VPN. In this example, enter **192.168.1.0/24**.
    -   **Client Subnet**: Enter a CIDR block to be used by the client to connect to the server. In this example, enter **10.10.10.0/24**.
    -   **Advanced Configuration**: In advanced settings, set the following parameters:
        -   **Protocol**: Select the protocol of SSL Certificates Service connections. Supported protocols include UDP and TCP. In this example, select the default protocol.
        -   **Port**: The port used in SSL Certificates Service connections. In this example, use the default port.
        -   **Encryption Algorithm**: The encryption algorithm used in SSL Certificates Service connections. Supported encryption algorithms include AES-128-CBC, AES-192-CBC, and AES-256-CBC. In this example, select the default algorithm.
        -   **Enable Compression**: Select whether to compress the transmitted data. In this example, use the default setting.
        -   **Two-factor Authentication**: Enable two-factor authentication and select an IDaaS instance.

            Alibaba Cloud Identity as a Service \(IDaaS\) is a unified identity authentication service. IDaaS allows one account to access all services. Two-factor authentication for the SSL dialing client is implemented after you create and select an IDaaS instance. Apart from certificate key authentication, you must complete two-factor authentication, where the user name and password are authenticated. After you pass them, a dial-up connection is initiated from the SSL client and you can access the resources deployed in the cloud.

            **Note:** If this is your first time using two-factor authentication, you must grant the VPN Gateway instance the permission to access the IDaaS instance before you create the SSL Certificates Service server.

    ![Enable two-factor authentication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6047325951/p88603.png)


## Optional. Step 3: Configure Active Directory \(AD\) authentication for cloud services.

By default, the user name and password of the IDaaS instance can be used for two-factor authentication. You can configure AD authentication. After you complete the configuration, SSL-VPN supports AD authentication. If you only use the user name and password of the IDaaS instance for authentication, skip this step.

1.  Log on to the as an administrator.

2.  On the **Instances** page, find the IDaaS instance you want to manage and click **Management** in the **Actions** column.

3.  In the left-side navigation pane, choose **Authentication** \> **Authentication Source** and click **Add Authentication Source**.

4.  In the **Add Authentication Source** dialog box that appears, find **LDAP** and click **Add Authentication Source** in the **Actions** column.

5.  In the **Add Authentication Source \(LDAP\)** dialog box that appears, create an LDAP authentication source.

    For more information, see [LDAP as Authentication Source]().

    After authentication sources are created, you can view them.

    ![The authentication source](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7047325951/p97766.png)

6.  On the **Authentication Source** page, find the authentication source that you want to manage, click ![Enable the authentication source](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7047325951/p97768.png) in the **Status** column, and then click **OK** in the dialog box that appears.

7.  In the left-side navigation pane, choose **Settings** \> **Security Settings**.

8.  On the **Security Settings** page, click the **Cloud product AD certification** tab.

9.  Select the AD authentication source that you have created, enable this feature, and then click **Save**.

    ![The authentication source](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7047325951/p97935.png)


## Step 4: Create and download an SSL Certificates Service client certificate

To create and download an SSL Certificates Service client certificate based on the SSL Certificates Service server configuration, follow these instructions:

1.  In the left-side navigation pane, choose **VPN** \> **SSL Clients**.

2.  On the top of the page, select the region of the SSL Certificates Service client.

    In this example, select **China \(Hangzhou\)**.

3.  On the **SSL Clients** page, click **Create Client Certificate**.

4.  On the **Create Client Certificate** page, configure the SSL Certificates Service client certificate based on the following information and click **OK**:

    -   **Name**: Enter a name for the SSL Certificates Service client certificate.
    -   **SSL Server**: Select the SSL Certificates Service server that you have created in step 2.
5.  On the **SSL Clients** page, find the created SSL Certificates Service client certificate, and click **Download** in the **Actions** column.

    The SSL Certificates Service client certificate is downloaded to your local device.


## Step 5: Configure the Linux client

To configure the Linux client, follow these instructions:

1.  Run the following command to install the OpenVPN client:

    ```
    yum install -y openvpn
    ```

2.  Extract the certificate from the package that has been downloaded in step 4 to /etc/openvpn/conf/.

3.  Run the following command to start the OpenVPN client, and then enter the user name and password for authentication.

    ```
    openvpn --config /etc/openvpn/conf/config.ovpn --daemon
    ```

    ![Start OpenVPN](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1927325951/p88600.png)


## Step 6: Test the connectivity

To test the connectivity between the Linux client and the VPC network, follow these instructions:

1.  Log on to the Linux client.

2.  Run the `ping` command to `ping` the IP address of the VPC-connected Elastic Computer Service \(ECS\) instance. This command tests the connectivity between the Linux client and VPC network.

    **Note:** Make sure that the security group rules of the ECS instance allow remote access from Linux clients. For more information, see [Scenarios for security groupsConfiguration guide for ECS security groups](/intl.en-US/Security/Security groups/Scenarios for security groups.md).

    The test result indicates that the Linux client can access the ECS instance.

    ![Test the connectivity](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7047325951/p88540.png)


