# Connect on-premises data centers to VPC networks

This topic describes how to create IPsec-VPN connections on VPN gateways to connect an on-premises data center to a Virtual Private Cloud \(VPC\) network.

Before you start, make sure that the following requirements are met:

-   An Alibaba Cloud account is created. If you do not have an Alibaba Cloud account, click [Create an Alibaba Cloud account](https://account.alibabacloud.com/register/intl_register.htm).
-   Check the gateway device in the on-premises data center. Alibaba Cloud VPN gateways support the standard IKEv1 and IKEv2 protocols. Any gateway device that supports these two protocols can connect to Alibaba Cloud VPN gateways, such as gateway devices manufactured by Huawei, H3C, Hillstone, Sangfor, Cisco ASA, Juniper, SonicWall, Nokia, IBM, and Ixia.
-   Make sure that you have set a static public IP address for the gateway device in the on-premises data center.
-   The CIDR block of the on-premises data center must not overlap with that of the VPC network.

For example, a company creates a VPC network on Alibaba Cloud. The CIDR block of the VPC network is 192.168.0.0/16. The CIDR block of the on-premises data center is 172.16.0.0/12. The static public IP address for the gateway device in the on-premises data center is 211.xx.xx.68. To meet business requirements, the company needs to connect the on-premises data center to the VPC network.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1222029951/p3312.png)

The preceding figure displays that the on-premises data center is connected to the VPC network through IPsec-VPN. Cloud resources can be shared with on-premises data centers.

## Step 1: Create a VPN gateway

Take the following steps to create a VPN gateway:

1.  Log on to the [VPN gateway console](https://vpc.console.aliyun.com/vpn).

2.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.

3.  On the **VPN Gateways** page, click **Create VPN Gateway**.

4.  On the buy page, set the following parameters, click **Buy Now**, and complete the payment.

    -   **Name**: Enter a name for the VPN gateway.
    -   **Region**: Select the region where you want to deploy the VPN gateway.

        **Note:** Make sure that the VPC network and the VPN gateway associated with the VPC network are deployed in the same region.

    -   **VPC**: Select the VPC network to be associated with the VPN gateway.
    -   **Bandwidth**: Specify the maximum bandwidth of the VPN gateway. The bandwidth is provided for data transfer over the Internet.
    -   **IPsec-VPN**: Specify whether to enable IPsec-VPN for the VPN gateway.
    -   **SSL-VPN**: Specify whether to enable SSL-VPN. SSL-VPN allows you to connect a client to a VPC network from any places.
    -   **SSL Connections**: Specify the maximum number of concurrent SSL connections that the VPN gateway supports.

        **Note:** This parameter is available only after SSL-VPN is enabled.

    -   **Billing Cycle**: Specify the subscription duration.
5.  Go to the VPN Gateways page to view the newly created VPN gateway.

    The newly created VPN gateway is in the Preparing state. Its status changes to Normal after about two minutes. The Normal state indicates that the VPN gateway is initialized and ready for use.

    **Note:** It takes about one to five minutes to create a VPN gateway.


## Step 2: Create a customer gateway

Take the following steps to create a customer gateway.

1.  In the left-side navigation pane, choose **VPN** \> **Customer Gateways**.

2.  Select the region where you want to deploy the customer gateway

3.  On the Customer Gateways page, click **Create Customer Gateway**.

4.  On the Create Customer Gateway page, set the following parameters, and then click **Submit**.

    -   **Name**: Enter a name for the customer gateway.
    -   **IP Address**: Enter the public IP address of the gateway device in the on-premises data center that is to be connected to the VPC network. In this example, enter **211.xx.xx.68**.
    -   **Description**: Enter a description for the customer gateway.

## Step 3: Create an IPsec-VPN connection

Take the following steps to create an IPsec-VPN connection:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.

2.  Select the region where you want to create an IPsec-VPN connection.

3.  On the IPsec Connections page, click **Create IPsec Connection**.

4.  On the Create IPsec Connection page, set the following parameters for the IPsec-VPN connection, and click **Submit**.

    -   **Name**: Enter a name for the IPsec-VPN connection.
    -   **VPN Gateway**: Select a VPN gateway.
    -   **Customer Gateway**: Select the customer gateway to be connected through the IPsec-VPN connection.
    -   **Source CIDR Block**: Enter the CIDR block of the VPC network with which the selected VPN gateway is associated. In this example, enter **192.168.0.0/16**.
    -   **Destination CIDR Block**: Enter the CIDR block of the on-premises data center. In this example, enter **172.16.0.0/12**.
    -   **Immediate Effect**: Specify whether to start connection negotiations immediately.
        -   **Yes**: negotiate immediately after the configuration is complete.
        -   **No**: negotiate when traffic is detected in the IPsec-VPN connection.
    -   **Pre-shared Key**: Enter the pre-shared key. The pre-shared key must be the same as that of the gateway device deployed in the on-premises data center.

        Use the default settings for other parameters.


## Step 4: Load the configurations of the IPsec-VPN connection to the customer gateway device

Take the following steps to load the configurations of the IPsec-VPN connection to the customer gateway device:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.

2.  Select the region where the IPsec-VPN connection is established.

3.  On the IPsec Connections page, find the target IPsec-VPN connection, and then choose **More** \> **Download Configuration** in the **Actions** column.

4.  Load the configurations of the IPsec-VPN connection to the customer gateway device by following the instructions described in [Configure customer gateways](/intl.en-US/User Guide/Configure IPsec-VPN connections/Configure local gateways/Configure an IPsec-VPN connection through a USG series Next-Generation Firewall device (Huawei).md). .

    RemotSubnet and LocalSubnet in the downloaded configurations are opposite to RemotSubnet and LocalSubnet that you specify when you create an IPsec-VPN connection. For a VPN gateway, RemotSubnet refers to the CIDR block of the on-premises data center and LocalSubnet refers to the CIDR block of the VPC network. For a customer gateway, LocalSubnet refers to the CIDR block of the on-premises data center and RemoteSubnet refers to the CIDR block of the VPC network.


## Step 5: Configure routes for the VPN gateway

Take the following steps to configure routes for the VPN gateway:

1.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.

2.  Select the region where the VPN gateway is deployed.

3.  On the VPN Gateways page, find the target VPN gateway, and then click the instance ID in the Instance ID/Name column.

4.  In the Destination-based routing tab, click **Add Route Entry**.

5.  In the Add Route Entry dialog box, set the following parameters and click **OK**.

    -   **Destination CIDR Block**: Enter the CIDR block of the on-premises data center. In this example, enter **172.16.0.0/12**.
    -   **Next Hop Type**: Select IPsec Connection.
    -   **Next Hop**: Select an IPsec instance.
    -   **Publish to VPC**: Specify whether to automatically publish new route entries to the VPC route table. In this example, select **Yes**.
    -   **Weight**: Select a weight. In this example, select **100**.

## Step 6: Verify the settings

Log on to an Elastic Compute Service \(ECS\) instance that is not assigned a public IP address in the VPC network. Run the ping command to ping the private IP address of a server that resides in the on-premises data center, and test the connectivity.

