# Access cloud resources in a classic network from a Mac client

This topic describes how to configure SSL-VPN on VPN gateways to access cloud resources deployed in a classic network from a Mac client.

If you have already configured an SSL-VPN connection on the client, skip to Step 5 to connect Elastic Compute Service \(ECS\) instances that are deployed in a classic network to a virtual private cloud \(VPC\).

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/13374/15688616253605_en-US.png)

## Prerequisites

Before you start, make sure that the following requirements are met:

-   The client can access the Internet.

-   To configure SSL-VPN, you must switch to the new console. For more information, see [Switch to the new console](https://help.aliyun.com/document_detail/66173.html?spm=a2c4g.11186623.2.3.KK5rNc).

-   We recommend that you create a new VPC and set the CIDR block of the VPC to 172.16.0.0/12. If you specify an existing VPC, make sure that the VPC meets the requirements in the following table.

|CIDR block of the VPC|Requirement|
|:--------------------|:----------|
|172.16.0.0/12|The VPC does not contain a custom route whose destination CIDR block is 10.0.0.0/8. You can log on to the VPC console and navigate to the route table details page to view the routes that are configured for the VPC. |
|192.168.0.0/16|-   The VPC does not contain a custom route whose destination CIDR block is 10.0.0.0/8.

-   A route is added for each ECS instance in the classic network. The route points 192.168.0.0/16 to the Elastic Network Interface \(ENI\) of the ECS instance. You can use the provided script to add the route. [Download the script](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/58095/cn_zh/1502878832385/route192.zip).

**Note:** Before you run the script, read the readme file in the downloaded package. |


## Step 1: Create a VPN gateway

If the VPN gateway is deployed in a VPC and you need to use the VPN gateway in a classic network, you can create a ClassicLink to connect the VPC and classic network.

Perform the following operations to create a VPN gateway:

1.  Log on to the new [VPC console](https://vpcnext.console.aliyun.com).
2.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
3.  On the VPN Gateways page, click **Create VPN Gateway**.
4.  Set the parameters on the buy page and complete the payment. Set the following parameters to create a VPN gateway:
    -   **Region**: Select the region where you want to deploy the VPN gateway. In this example, **China \(Hangzhou\)** is selected.

**Note:** Make sure that the VPN gateway and the VPC for which the VPN gateway is created are deployed in the same region.

    -   **VPC**: Select the VPC for which the VPN gateway is created.

    -   **Bandwidth**: Specify the maximum bandwidth for the VPN gateway. The bandwidth is provided for data transfer over the Internet.

    -   **IPsec-VPN**: Specify whether to enable IPsec-VPN for the VPN gateway. If you enable IPsec-VPN, you can use the VPN gateway to create IPsec-VPN connections.

    -   **SSL-VPN**: Specify whether to enable SSL-VPN. In this example, **Enable** is selected.

    -   **SSL Connections**: Specify the maximum number of concurrent SSL connections that the VPN gateway supports.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/13374/15688616253606_en-US.png)

5.  Navigate to the VPN Gateways page to view the newly created VPN gateway.

    The newly created VPN gateway is in the Preparing state. The VPN gateway changes to the Normal state after about two minutes. If the state of the VPN gateway is Normal, it indicates that the VPN gateway is initialized and ready for use.

    **Note:** It takes about one to five minutes to create a VPN gateway.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/13374/15688616273607_en-US.png)


## Step 2: Create an SSL server

Perform the following operations to create an SSL server:

1.  In the left-side navigation pane, choose **VPN** \> **SSL Servers**.
2.  Click **Create SSL Server**. Set the following parameters to create an SSL server:
    -   **Name**: Enter a name for the SSL server.

    -   **VPN Gateway**: Select the VPN gateway that you created in Step 1 from the drop-down list.

    -   **Local Network**: **Enter the private CIDR block of the ECS instance that is deployed in the classic network that you want to access**. Click **Add Local Network** to add more CIDR blocks.

        In this example, 10.1.0.0/16 and 10.2.0.0/16 are added.

        **Note:** If the IP address of the ECS instance does not fall within the added private CIDR blocks, you must add the private CIDR block to which the IP address of the ECS instance belongs.

    -   **Client CIDR Block**: **Enter the CIDR block that is used by the client to connect to the SSL server. The client CIDR block must fall within the CIDR block of the VPC to which the VPN gateway belongs.**

        In this example, the client CIDR block is 172.16.10.0/24.

        **Note:** The client CIDR block does not refer to the CIDR block of the client. The client CIDR block is used to allocate IP addresses to the client. After the client is assigned an IP address, it can remotely access resources through an SSL-VPN connection.

    -   **Advanced Configuration**: In this example, the default setting is used.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/13374/15688616313608_en-US.png)


## Step 3: Create an SSL client certificate

Perform the following operations to create an SSL client certificate:

1.  In the left-side navigation pane, choose **VPN** \> **SSL Clients**.
2.  Click **Create Client Certificate**.
3.  In the Create Client Certificate dialog box, enter a name for the SSL client certificate, select the SSL server to which the SSL client certificate is to be imported, and then click **OK**.
4.  On the SSL Clients page, find the SSL client certificate that you created, and click **Download** to download the SSL client certificate.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/13374/15688616343609_en-US.png)


## Step 4: Configure the client

Perform the following operations to configure the client:

1.  Run the following command to install OpenVPN:

    ```
    brew install openvpn
    ```

    **Note:** Make sure that homebrew is installed before you install OpenVPN.

2.  Decompress the SSL client certificate package that you downloaded in Step 3 and copy the SSL client certificate file to the folder where OpenVPN is installed. Then, initiate an SSL-VPN connection.
    1.  Backup the default configuration file, and then run the following command to delete the default configuration file:

        ```
        rm /usr/local/etc/openvpn/*
        ```

    2.  Run the following command to copy the file to the configuration directory:

        ```
        cp cert_location /usr/local/etc/openvpn/
        ```

        In the preceding command, `cert_location` represents the path that stores the SSL client certificate downloaded in Step 3. For example, /Users/example/Downloads/certs6.zip is the path to the SSL client certificate.

    3.  Run the following command to decompress the SSL client certificate package:

        ```
        unzip /usr/local/etc/openvpn/certs6.zip
        ```

    4.  Run the following command to initiate a connection:

        ```
        sudo /usr/local/opt/openvpn/sbin/openvpn --config /usr/local/etc/openvpn/config.ovpn
        ```


## Step 5: Establish a ClassicLink

Perform the following operations to establish a ClassicLink:

1.  Log on to the VPC console.
2.  Select the region where the VPC is deployed and click the ID of the VPC.
3.  On the VPC Details page, click **Enable ClassicLink**.
4.  In the message that appears, click **OK**.
5.  Log on to the ECS console.
6.  In the left-side navigation pane, click **Instances**.
7.  Select one or more ECS instances deployed in the classic network that you want to access, and choose **More** \> **Connect to VPC**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/13374/15688616353610_en-US.png)

8.  In the dialog box that appears, specify the VPC that you want to connect, and click **OK**.
9.  In the left-side navigation pane, choose **Networks and Security** \> **Security Groups**.
10. On the Security Groups page, click the **Inbound** tab, and then click **Add Security Group Rule**. Set the following parameters to configure the security group:
    -   **Rule Direction**: Inbound

    -   **Action**: Allow

    -   **Protocol Type**: All

    -   **Authorization Type**: IPv4 CIDR Block

    -   **Authorization Object**: Enter the private IP address \(for example, 172.16.3.44/32\) that needs to access the ECS instance through the VPN gateway.

        Run the ifconfig command on the Mac client, and then find the information that is similar to `inet 172.16.10.6 --> 172.16.10.5 netmask 0xffffffff`. `172.16.10.6` is the IP address of the client. This is also the authorization object configured for the security group.

        **Note:** If you fail to access the ECS instance through the VPN gateway, it indicates that the client IP address has changed and you must add a new security group rule.

11. Navigate to the Instances page of the ECS console, click the Column Filters icon in the upper-right corner. In the dialog box that appears, select **Connection Status**, and click **OK**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/13374/15688616333611_en-US.png)

12. You can view the state of the connection established to the ECS instance.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/13374/15688616403612_en-US.png)

    If the connection is in the Connected state, it indicates that you can access the applications on the ECS instance from the Mac client.


