# Establish IPsec-VPN connections between two VPCs

This topic describes how to establish IPsec-VPN connections between two virtual private clouds \(VPCs\) to enable resources in the VPCs to access each other.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5133177951/p3319.png)

This example shows how to establish IPsec-VPN connections between two VPCs under the same account. You can also establish IPsec-VPN connections between two VPCs under different accounts by following the same procedure. Note that if you want to establish IPsec-VPN connections between two VPCs under different accounts, make sure that you have the public IP address of the peer VPN gateway from the other account. The public IP address of the peer VPN gateway is used to create a customer gateway.

|VPC name|VPC CIDR block|VPC ID|ECS instance name|
|:-------|:-------------|:-----|:----------------|
|VPC1|172.16.0.0/12|vpc-xxxxz0|ECS1|
|VPC2|10.0.0.0/8|vpc-xxxxut|ECS2|

**Note:** VPN gateways are used to enable encrypted data transmission over the Internet. The communication performance depends on the quality of the Internet connection. If you require higher communication quality, we recommend that you use Cloud Enterprise Network \(CEN\) to connect your networks. For more information about how to use CEN to connect networks, see [Plan your CEN]().

## Before you start

Make sure that the private IP addresses of the two VPCs do not overlap with each other.

## Step 1: Create a VPN gateway

Perform the following operations to create a VPN gateway:

1.  Log on to the [VPC console](https://vpcnext.console.aliyun.com/nat/).
2.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
3.  On the VPN Gateways page, click **Create VPN Gateway**.
4.  On the buy page, set the following parameters, click **Buy Now**, and complete the payment.
    -   **Name**: Enter a name for the VPN gateway.
    -   **Region**: Select the region where you want to deploy the VPN gateway.

        **Note:** Make sure that the VPC and the VPN gateway for the VPC are deployed in the same region.

    -   **VPC**: Select the VPC to be associated with the VPN gateway.
    -   **Bandwidth**: Specify the maximum bandwidth of the VPN gateway. The bandwidth is provided for data transfer over the Internet.
    -   **IPsec-VPN**: Specify whether to enable IPsec-VPN for the VPN gateway.
    -   **SSL-VPN**: Specify whether to enable SSL-VPN for the VPN gateway. SSL-VPN allows you to connect a client to a VPC from any locations.
    -   **SSL Connections**: Specify the maximum number of concurrent SSL connections that the VPN gateway supports.

        **Note:** This parameter is available only after SSL-VPN is enabled.

    -   **Billing Cycle**: Specify the subscription duration.
5.  Repeat the preceding steps to create a VPN gateway for the other VPC.

    The newly created VPN gateway is in the Preparing state. After about two minutes, the state changes to Normal. If the VPN gateway is in the Normal state, it indicates that the VPN gateway is initialized and ready for use. After the VPN gateway is created, a public IP address is assigned to the VPN gateway.

    **Note:** It takes about one to five minutes to create a VPN gateway.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5133177951/p3320.png)

    In this example, the public IP addresses that are assigned to the two VPN gateways are 121.xxx.xx.143 and 118.xxx.xx.149. The following table lists the details of the VPN gateways, VPCs, and public IP addresses.

    |VPC|VPN gateway|Public IP address|
    |:--|:----------|:----------------|
    |Name: VPC 1

 ID: vpc-xxxxz0

 CIDR block: 172.16.0.0/12

|vpn-xxxxxqwj|118.xxx.xx.149|
    |Name: VPC 2

 ID: vpc-xxxxut

 CIDR block: 10.0.0.0/8

|vpn-xxxxxl5z|121.xxx.xx.143|


## Step 2: Create a customer gateway

Perform the following operations to create a customer gateway.

1.  In the left-side navigation pane, choose **VPN** \> **Customer Gateways**.
2.  Select the region where you want to deploy the customer gateway.
3.  On the Customer Gateways page, click **Create Customer Gateway**.
4.  On the Create Customer Gateway page, set the following parameters, and click **OK**.
    -   **Name**: Enter a name for the customer gateway.
    -   **IP Address**: Enter the public IP address of the gateway device in the on-premises data center to be connected to the VPC.
    -   **Description**: Enter a description for the customer gateway.
5.  Repeat the preceding operations to create another customer gateway with another public IP address.

    The following table lists the details of the VPCs, VPN gateways, and customer gateways.

    |VPC|VPN gateway|Public IP address|Customer gateway|
    |:--|:----------|:----------------|:---------------|
    |Name: VPC 1

 ID: vpc-xxxxz0

 CIDR block: 172.16.0.0/12

|vpn-xxxxxqwj|121.xxx.xx.143|user\_VPC1|
    |Name: VPC 2

 ID: vpc-xxxxut

 CIDR block: 10.0.0.0/8

|vpn-xxxxxl5z|118.xxx.xx.149|user\_VPC|


## Step 3: Create an IPsec-VPN connection

After you create the VPN gateways and customer gateways, you can create IPsec-VPN connections to connect the VPN gateways with customer gateways.

1.  In the left-side navigation pane, choose **VPN** \> **IPsec Connections**.
2.  Select the region where you want to create an IPsec-VPN connection.
3.  On the IPsec Connections page, click **Create IPsec Connection**.
4.  On the Create IPsec Connection page, set the following parameters for the IPsec-VPN connection, and click **OK**.
    -   **Name**: Enter a name for the IPsec-VPN connection.
    -   **VPN Gateway**: Select one of the two VPN gateways that you created in Step 1. In this example, the vpn-xxxxxqwj VPN gateway that is associated with VPC 1 is selected.
    -   **Customer Gateway**: Select the customer gateway to be connected through the IPsec-VPN connection. In this example, the user\_VPC 2 customer gateway is selected.
    -   **Source CIDR Block**: Enter the CIDR block of the VPC with which the selected VPN gateway is associated. In this example, 172.16.0.0/12 is entered.
    -   **Destination CIDR Block**: Enter the CIDR block of the VPC to be connected. In this example, the CIDR block of VPC 2 is entered, which is 10.0.0.0/8.
    -   **Immediate Effect**: Specify whether to start connection negotiations immediately.
        -   Yes: Negotiates immediately after the configuration is completed.
        -   No: Negotiates when data transfer is detected.
    -   **Pre-shared Key**: Enter the pre-shared key. In this example, 1234567 is entered. You must set the same pre-shared key for both IPsec-VPN connections.
    -   **Health Check**: Enable health checks, and enter the destination IP address, source IP address, retry interval, and number of retries.

        Use the default settings for other parameters.

5.  Repeat the preceding operations to create an IPsec-VPN connection for VPC 2.

## Step 5: Configure routes for each VPN gateway

Perform the following operations to configure a route for each VPN gateway.

1.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.
2.  Select the region where the VPN gateway is deployed.
3.  On the VPN Gateways page, find the VPN gateway for which you want to configure routes, and click its ID in the Instance ID/Name column.
4.  In the Destination-based routing tab, click **Add Route Entry**.
5.  In the Add Route Entry dialog box, set the following parameters, and click **OK**.
    -   **Destination CIDR Block**: Enter the CIDR block of VPC 2.
    -   **Next Hop**: Select an IPsec connection.
    -   **Publish to VPC**: Specify whether to automatically publish new routes to the VPC route table. In this example, Yes is selected.
    -   **Weight**: Specify a weight. In this example, 100 is entered.
6.  Repeat the preceding operations to configure a route for the other VPN gateway.

## Step 5: Test the connectivity

Log on to ECS 1 in VPC 1, and then ping the private IP address of ECS 2 in VPC 2 \(ECS 2\) to test the connectivty.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5133177951/p3323.png)

