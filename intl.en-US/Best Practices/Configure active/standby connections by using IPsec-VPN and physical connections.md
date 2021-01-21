# Configure active/standby connections by using IPsec-VPN and physical connections

This topic describes how to configure active/standby connections by using IPsec-VPN connections and physical connections that are provided by Express Connect. You can establish active/standby connections for applications to ensure that the applications are highly available.

You can connect an on-premises network to a virtual private cloud \(VPC\) through a physical connection or an IPsec-VPN connection.

-   When the physical connection is active, data between the on-premises network and VPC is transmitted through the physical connection.
-   When the physical connection is down, data between the on-premises network and VPC is transmitted through the IPsec-VPN connection.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0612397751/p41822.png)

## Prerequisites

A physical connection is established from the on-premises network to the VPC. For more information, see [Create a dedicated physical connection](/intl.en-US/Physical Connection/Dedicated physical connection/Create a dedicated physical connection.md).

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

Perform the following operations to create an IPsec-VPN connection:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.
2.  Select the region where you want to create the IPsec-VPN connection.
3.  On the IPsec Connections page, click **Create IPsec Connection**.
4.  Set the following parameters based on the following information and click **OK**:
    -   **Name**: Enter a name for the IPsec-VPN connection.
    -   **VPN Gateway**: Select a VPN gateway from the drop-down list.
    -   **Customer Gateway**: Select the customer gateway to be connected through the IPsec-VPN connection.
    -   **Local Network**: Enter the CIDR block of the VPC where the VPN gateway is deployed.
    -   **Remote Network**: Enter the CIDR block of the on-premises network.
    -   **Effective Immediately**: Specify whether to immediately start negotiations.
        -   Yes: immediately negotiates after the configuration is completed.
        -   No: negotiates when traffic is detected.
    -   **Pre-Shared Key**: Enter the pre-shared key. The pre-shared key must be the same as the one specified on the gateway device.
    -   **Health Check**: Enable health checks, and specify the destination IP address, source IP address, retry interval, and number of retries.

        Use the default settings for other parameters.


## Step 4: Load the configurations of the IPsec-VPN connection to the customer gateway device

Take the following steps to load the configurations of the IPsec-VPN connection to the customer gateway device:

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.

2.  Select the region where the IPsec-VPN connection is established.

3.  On the IPsec Connections page, find the target IPsec-VPN connection, and then choose **More** \> **Download Configuration** in the **Actions** column.

4.  Load the configurations of the IPsec-VPN connection to the customer gateway device by following the instructions described in [Configure customer gateways](/intl.en-US/User Guide/Configure IPsec-VPN connections/Configure local gateways/Load the IPsec-VPN configuration to a Huawei firewall device.md). .

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

## Step 6: Enable health checks for the VBR of the physical connection

You must enable health checks for the virtual border router \(VBR\) of the physical connection. This way, the status of the physical connection can be detected from the VPC. When the physical connection is down, data is transferred through the IPsec-VPN connection.

For more information, see [Configure health checks](/intl.en-US/Common Configurations/Configure health checks.md).

## Step 7: Configure the gateway device

You must configure an active route and a standby route on the gateway device. Both routes point to the VPC. You also need to enable health checks to detect the status of the physical connection. When the physical connection is down, data is transferred through the IPsec-VPN connection.

