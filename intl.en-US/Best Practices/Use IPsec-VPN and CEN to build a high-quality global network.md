# Use IPsec-VPN and CEN to build a high-quality global network

This topic describes how to use VPN Gateway and Cloud Enterprise Network \(CEN\) to connect on-premises data centers to Alibaba Cloud and build a cross-border enterprise network that is high quality and cost-effective.

Before you start, make sure that the following requirements are met:

-   Virtual private clouds \(VPCs\) are created, and applications are deployed in the VPCs. For more information, see [Create a VPC](/intl.en-US/VPCs and VSwitches/VPC management/Create a VPC.md).
-   A gateway device is deployed in each office and a static public IP address is allocated to each gateway device.
-   A CEN instance is created. For more information, see [Create a CEN instance]().
-   A CEN bandwidth plan is purchased and the bandwidth is allocated for cross-region communication. For more information, see [Purchase a bandwidth package]() and [Configure a cross-region connection bandwidth]().
-   The CIDR blocks that are used to create connections must not overlap with each other.

![Background](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6005416751/p71284.png)

An international company has two offices in the US \(Silicon Valley\) region and two in the China \(Shanghai\) region. The company has created VPC 1 in the US \(Silicon Valley\) region and VPC 2 in the China \(Shanghai\) region. An application is deployed in each VPC. Due to business development, the company must connect the following networks: the networks of the offices in the US \(Silicon Valley\) region, the networks of the offices in the China \(Shanghai\) region, VPC 1, and VPC 2. The following table describes the CIDR blocks of the networks.

|Network|CIDR block|
|-------|----------|
|Office 1 in US \(Silicon Valley\)|10.10.10.0/24|
|Office 2 in US \(Silicon Valley\)|10.10.20.0/24|
|VPC 1 in US \(Silicon Valley\)|172.16.0.0/16|
|Office 3 in China \(Shanghai\)|10.20.10.0/24|
|Office 4 in China \(Shanghai\)|10.20.20.0/24|
|VPC 2 in China \(Shanghai\)|192.168.0.0/16|

![IPsec](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6005416751/p71231.png)

You can use VPN gateway 1 to connect Office 1 and Office 2 to VPC 1, and use VPN gateway 2 to connect Office 3 and Office 4 to VPC 2, as shown in the preceding figure. Then, you can attach VPC 1 and VPC 2 to the same CEN instance to enable cross-border communication.

The following flowchart shows the procedure.

![Procedure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7005416751/p71275.png)

## Step 1: Create IPsec-VPN connections to the offices in the US \(Silicon Valley\) region

To create IPsec-VPN connections in the US \(Silicon Valley\) region to connect Office 1 and Office 2 to VPC 1, perform the following operations:

1.  Create a VPN gateway for the VPC in the US \(Silicon Valley\) region.

    Set the following parameters to create the VPN gateway:

    -   **Name**: Enter a name for the VPN gateway. In this example, VPN gateway 1 is entered.
    -   **Region**: Select the US \(Silicon Valley\) region.
    -   **VPC**: Select the VPC in the US \(Silicon Valley\) region.
    -   **Peak Bandwidth**: Specify the maximum bandwidth. In this example, 5 Mbit/s is specified.
    -   **IPsec-VPN**: Enable IPsec-VPN for the VPN gateway.
    -   **SSL-VPN**: Disable SSL-VPN.
    For more information, see [Create a VPN gateway](/intl.en-US/User Guide/Manage a VPN Gateway/Create a VPN gateway.md).

2.  Create two customer gateways and register the public IP addresses of the gateway devices in Office 1 and Office 2 to the customer gateways. The public IP addresses are used to create IPsec-VPN connections.

    Set the following parameters to create a customer gateway for Office 1:

    -   **Name**: Enter a name for the customer gateway. In this example, Customer gateway 1 is entered.
    -   **IP Address**: Enter the static public IP address of the gateway device in Office 1. In this example, 1.1.1.1 is entered.
    Set the following parameters to create a customer gateway for Office 2:

    -   **Name**: Enter a name for the customer gateway. In this example, Customer gateway 2 is entered.
    -   **IP Address**: Enter the static public IP address of the gateway device in Office 2. In this example, 2.2.2.2 is entered.
    For more information, see [Create a customer gateway](/intl.en-US/User Guide/Manage a customer gateway/Create a customer gateway.md).

3.  Create two IPsec-VPN connections to connect the gateway devices in Office 1 and Office 2 to the VPN gateway.

    Set the following parameters to create an IPsec-VPN connection between Office 1 and the VPN gateway:

    -   **Name**: Enter a name for the IPsec-VPN connection. In this example, IPsec-VPN connection 1 is entered.
    -   **VPN Gateway**: Select the VPN gateway that is created for the VPC in the US \(Silicon Valley\) region. In this example. VPN gateway 1 is selected.
    -   **Customer Gateway**: Select the customer gateway to be connected to the VPN gateway. In this example, Customer gateway 1 is selected.
    -   **Local Network**: Enter the CIDR block of the VPC to be connected to the office. In this example, 172.16.0.0/16 is entered.
    -   **Remote Network**: Enter the CIDR block of Office 1 to be connected to the VPC. In this example, 10.10.10.0/24 is entered.
    -   **Effective Immediately**: Specify whether to negotiate immediately. In this example, Yes is selected.
        -   **Yes**: negotiates immediately after the configuration is completed.
        -   **No**: negotiates when data transfer is detected.
    -   **Pre-Shared Key**: Enter a pre-shared key for identity verification between VPN gateway 1 and Customer gateway 1. In this example, 123456 is entered.
    Use the default settings for other parameters.

    Set the following parameters to create an IPsec-VPN connection between Office 2 and the VPN gateway:

    -   **Name**: Enter a name for the IPsec-VPN connection. In this example, IPsec-VPN connection 2 is entered.
    -   **VPN Gateway**: Select the VPN gateway that is created for the VPC in the US \(Silicon Valley\) region. In this example, VPN gateway 1 is selected.
    -   **Customer Gateway**: Select the customer gateway that is created for Office 2. In this example, Customer gateway 2 is selected.
    -   **Local Network**: Enter the CIDR block of the VPC to be connected to the office. In this example, 172.16.0.0/16 is entered.
    -   **Remote Network**: Enter the CIDR block of Office 2 to be connected to the VPC. In this example, 10.10.20.0/24 is entered.
    -   **Effective Immediately**: Specify whether to negotiate immediately. In this example, Yes is selected.
        -   **Yes**: negotiates immediately after the configuration is completed.
        -   **No**: negotiates when data transfer is detected.
    -   **Pre-Shared Key**: Enter a pre-shared key for identity verification between VPN gateway 1 and Customer gateway 2. In this example, 654321 is entered.
    Use the default settings for other parameters.

    For more information, see [Create an IPsec-VPN connection](/intl.en-US/User Guide/Configure IPsec-VPN connections/Manage an IPsec-VPN connection/Create an IPsec-VPN connection.md).

4.  Load the configurations of the IPsec-VPN connections to the gateway devices in Office 1 and Office 2.

    For more information, see [Configure gateway devices](/intl.en-US/User Guide/Configure IPsec-VPN connections/Configure local gateways/Configure an IPsec-VPN connection through a USG series Next-Generation Firewall device (Huawei).md).

5.  Configure routes on VPN gateway 1.

    Configure the following route on VPN gateway 1 to route network traffic that is destined for Office 1:

    -   **Destination CIDR Block**: Enter the private CIDR block of Office 1. In this example, 10.10.10.0/24 is entered.
    -   **Next Hop Type**: Select IPsec Connection.
    -   **Next Hop**: Select an IPsec-VPN connection. In this example, IPsec-VPN connection 1 is selected.
    -   **Publish to VPC**: Specify whether to automatically advertise this route to the route table of the VPC. In this example, Yes is selected.
        -   Yes: automatically advertises the route to the route table of the VPC. We recommend that you select Yes.
        -   No: does not advertise the route to the route table of the VPC.
    -   **Weight**: Specify a weight. In this example, 0 is specified.
    Configure the following route on VPN gateway 1 to route network traffic that is destined for Office 2:

    -   **Destination CIDR Block**: Enter the private CIDR block of Office 2. In this example, 10.10.20.0/24 is entered.
    -   **Next Hop Type**: Select IPsec Connection.
    -   **Next Hop**: Select an IPsec-VPN connection. In this example, IPsec-VPN connection 2 is selected.
    -   **Publish to VPC**: Specify whether to automatically advertise this route to the route table of the VPC.
        -   Yes: automatically advertises the route to the route table of the VPC. We recommend that you select Yes.
        -   No: does not advertise the route to the route table of the VPC.
    -   **Weight**: Specify a weight. In this example, 0 is specified.
    The following figure shows the route tables of Office 1, Office 2, VPN gateway 1, and VPC 1.

    ![Route tables of Office 1, Office 2, VPN gateway 1, and VPC 1.](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7005416751/p71263.png)


## Step 2: Create IPsec-VPN connections to the offices in the China \(Shanghai\) region

To create IPsec-VPN connections in the China \(Shanghai\) region to connect Office 3 and Office 4 to VPC 2, perform the following operations:

1.  Create a VPN gateway for the VPC in the China \(Shanghai\) region.

    Set the following parameters to create the VPN gateway:

    -   **Name**: Enter a name for the VPN gateway. In this example, VPN gateway 2 is entered.
    -   **Region**: Select the China \(Shanghai\) region.
    -   **VPC**: Select the VPC in the China \(Shanghai\) region.
    -   **Peak Bandwidth**: Specify the maximum bandwidth. In this example, 5 Mbit/s is specified.
    -   **IPsec-VPN**: Enable IPsec-VPN for the VPN gateway.
    -   **SSL-VPN**: Disable SSL-VPN.
    For more information, see [Create a VPN gateway](/intl.en-US/User Guide/Manage a VPN Gateway/Create a VPN gateway.md).

2.  Create two customer gateways and register the public IP addresses of the gateway devices in Office 3 and Office 4 to the customer gateways. The public IP addresses are used to create IPsec-VPN connections.

    Set the following parameters to create a customer gateway for Office 3:

    -   **Name**: Enter a name for the customer gateway of Office 3. In this example, Customer gateway 3 is entered.
    -   **IP Address**: Enter the static public IP address of the gateway device in Office 3. In this example, 3.3.3.3 is entered.
    Set the following parameters to create a customer gateway for Office 4:

    -   **Name**: Enter a name for the customer gateway of Office 4. In this example, Customer gateway 4 is entered.
    -   **IP Address**: Enter the static public IP address of the gateway device in Office 4. In this example, 4.4.4.4 is entered.
    For more information, see [Create a customer gateway](/intl.en-US/User Guide/Manage a customer gateway/Create a customer gateway.md).

3.  Create two IPsec-VPN connections to connect the gateway devices of Office 3 and Office 4 to the VPN gateway.

    Set the following parameters to create an IPsec-VPN connection between Office 3 and the VPN gateway:

    -   **Name**: Enter a name for the IPsec-VPN connection. In this example, IPsec-VPN connection 3 is entered.
    -   **VPN Gateway**: Select the VPN gateway that is created for the VPC in the China \(Shanghai\) region. In this example. VPN gateway 2 is selected.
    -   **Customer Gateway**: Select the customer gateway that is created for Office 3. In this example, Customer gateway 3 is selected.
    -   **Local Network**: Enter the CIDR block of the VPC to be connected to the office. In this example, 192.168.0.0/16 is entered.
    -   **Remote Network**: Enter the CIDR block of Office 3 to be connected to the VPC. In this example, 10.20.10.0/24 is entered.
    -   **Effective Immediately**: Specify whether to negotiate immediately. In this example, Yes is selected.
        -   **Yes**: negotiates immediately after the configuration is completed.
        -   **No**: negotiates when data transfer is detected.
    -   **Pre-Shared Key**: Enter a pre-shared key for identity verification between VPN gateway 2 and Customer gateway 3. In this example, 123456 is entered.
    Use the default settings for other parameters.

    Set the following parameters to create an IPsec-VPN connection between Office 4 and the VPN gateway:

    -   **Name**: Enter a name for the IPsec-VPN connection. In this example, IPsec-VPN connection 4 is entered.
    -   **VPN Gateway**: Select the VPN gateway that is created for the VPC in the China \(Shanghai\) region. In this example, VPN gateway 2 is selected.
    -   **Customer Gateway**: Select the customer gateway that is created for Office 4. In this example, Customer gateway 4 is selected.
    -   **Local Network**: Enter the CIDR block of the VPC to be connected to the office. In this example, 192.168.0.0/16 is entered.
    -   **Remote Network**: Enter the CIDR block of Office 4 to be connected to the VPC. In this example, 10.20.20.0/24 is entered.
    -   **Effective Immediately**: Specify whether to negotiate immediately. In this example, Yes is selected.
        -   **Yes**: negotiates immediately after the configuration is completed.
        -   **No**: negotiates when data transfer is detected.
    -   **Pre-Shared Key**: Enter a pre-shared key for identity verification between VPN gateway 2 and Customer gateway 4. In this example, 654321 is entered.
    Use the default settings for other parameters.

    For more information, see [Create an IPsec-VPN connection](/intl.en-US/User Guide/Configure IPsec-VPN connections/Manage an IPsec-VPN connection/Create an IPsec-VPN connection.md).

4.  Load the configurations of the IPsec-VPN connections to the gateway devices in Office 3 and Office 4.

    For more information, see [Configure gateway devices](/intl.en-US/User Guide/Configure IPsec-VPN connections/Configure local gateways/Configure an IPsec-VPN connection through a USG series Next-Generation Firewall device (Huawei).md).

5.  Configure routes on VPN gateway 2.

    Configure the following route on VPN gateway 2 to route network traffic that is destined for Office 3:

    -   **Destination CIDR Block**: Enter the private CIDR block of Office 3. In this example, 10.20.10.0/24 is entered.
    -   **Next Hop Type**: Select IPsec Connection.
    -   **Next Hop**: Select an IPsec-VPN connection. In this example, IPsec-VPN connection 3 is selected.
    -   **Publish to VPC**: Specify whether to automatically advertise this route to the route table of the VPC.
        -   Yes: automatically advertises the route to the route table of the VPC. We recommend that you select Yes.
        -   No: does not advertise the route to the route table of the VPC.
    -   **Weight**: Specify a weight. In this example, 0 is specified.
    Configure the following route on VPN gateway 2 to route network traffic that is destined for Office 4:

    -   **Destination CIDR Block**: Enter the private CIDR block of Office 4. In this example, 10.20.20.0/24 is entered.
    -   **Next Hop Type**: Select IPsec Connection.
    -   **Next Hop**: Select an IPsec-VPN connection. In this example, IPsec-VPN connection 4 is selected.
    -   **Publish to VPC**: Specify whether to automatically advertise this route to the route table of the VPC.
        -   Yes: automatically advertises the route to the route table of the VPC.
        -   No: does not advertise the route to the route table of the VPC.
    -   **Weight**: Specify a weight. In this example, 0 is specified.
    The following figure shows the route tables of Office 3, Office 4, VPN gateway 2, and VPC 2.

    ![Route tables of Office 3, Office 4, VPN gateway 2, and VPC 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7005416751/p71264.png)


## Step 3: Attach the VPCs to a CEN instance

After you connect the offices to the VPCs, you must attach VPC 1 and VPC 2 to the same CEN instance so that the VPCs can communicate with each other.

1.  Log on to the [CEN console](https://cen.console.aliyun.com).

2.  On the Instances page, find the CEN instance to which you want to attach the VPCs and click the ID of the CEN instance.

3.  On the Networks tab, click **Attach Network**.

4.  Click the Your account tab.

5.  Attach the VPC to the CEN instance based on the following information, and click **OK**:

    -   **Network Type**: Select **VPC**.
    -   **Region**: Select **US \(Silicon Valley\)**.
    -   **Networks**: Select VPC 1.
6.  Repeat the preceding operations to attach VPC 2 to the same CEN instance.


## Step 4: Advertise routes to the CEN instance

To enable other VPCs that are attached to the CEN instance to learn the routes that point to the offices, you must advertise the routes of the VPCs in the US \(Silicon Valley\) and China \(Shanghai\) regions to the CEN instance. These routes point to the VPN gateways that are created for the VPCs. For more information, see [Publish a route to CEN]().

After the routes are advertised to the CEN instance, the route table of the CEN instance contains the following routes.

![Route table of the CEN instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7005416751/p71265.png)

## Step 5: Configure routes on the gateway devices

After the routes are advertised to the CEN instance, you must configure routes on the gateway devices of the offices in the US \(Silicon Valley\) region to route network traffic to the offices in the China \(Shanghai\) region. You must also configure routes on the gateway devices of the offices in the China \(Shanghai\) region to route network traffic to the offices in the US \(Silicon Valley\) region.

The configurations in the following table are for reference only. The configurations may vary based on the manufacturer of the gateway devices.

|Office|Route|
|------|-----|
|Office 1|```
ip route 192.168.0.0/16 5.5.5.5
ip route 10.20.10.0/24 5.5.5.5
ip route 10.20.20.0/24 5.5.5.5
ip route 10.10.20.0/24 5.5.5.5   #5.5.5.5 is the public IP address of VPN gateway 1.
``` |
|Office 2|```
ip route 192.168.0.0/16 5.5.5.5
ip route 10.20.10.0/24 5.5.5.5
ip route 10.20.20.0/24 5.5.5.5
ip route 10.10.10.0/24 5.5.5.5   #5.5.5.5 is the public IP address of VPN gateway 1.
``` |
|Office 3|```
ip route 172.16.0.0/16 6.6.6.6
ip route 10.10.10.0/24 6.6.6.6
ip route 10.10.20.0/24 6.6.6.6
ip route 10.20.20.0/24 6.6.6.6   #6.6.6.6 is the public IP address of VPN gateway 2.
``` |
|Office 4|```
ip route 172.16.0.0/16 6.6.6.6
ip route 10.10.10.0/24 6.6.6.6
ip route 10.10.20.0/24 6.6.6.6
ip route 10.20.10.0/24 6.6.6.6   #6.6.6.6 is the public IP address of VPN gateway 2.
``` |

The route tables of the offices are shown in the following figure.

![Route tables of the offices](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7005416751/p71266.png)

## Step 6: Test the connectivity

In this example, a PC in Office 1 is used to access the PCs in Office 2, Office 3, and Office 4 to test the connectivity.

1.  Open the command prompt on the PC in Office 1.

2.  Run the `ping` command to ping the PCs in Office 2, Office 3, and Office 4. If all responses are received, it indicates that the connections are established.


