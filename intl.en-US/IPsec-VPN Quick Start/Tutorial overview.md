# Tutorial overview

This topic describes how to connect a VPC to an on-premises data center through IPsec-VPN.

## Prerequisites

Before creating a site-to-site VPN connection, make sure the following conditions are met:

-   The protocols IKEv1 and IKEv2 are supported by the gateway device of the on-premises data center.

    IPsec-VPN supports IKEv1 and IKEv2 protocols. Devices that support these two protocols can connect to Alibaba Cloud VPN Gateway, including devices of Huawei, H3C, Hillstone, SANGFOR, Cisco ASA, Juniper, SonicWall, Nokia, IBM, and Ixia.

-   A static public IP address is configured for the local gateway.
-   The IP address ranges of the VPC and on-premises data center to be connected do not conflict with each other.

## Procedure

The following figure shows the procedure of connecting a VPC to an on-premises data center through IPsec-VPN.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8322029951/p40525.png)

1.  Create a VPN Gateway

    Enable the IPsec-VPN function. Up to 10 IPsec-VPN connections can be established in a VPN Gateway.

2.  Create a customer gateway

    By creating a customer gateway, you can register the local gateway to Alibaba Cloud and connect the customer gateway to the VPN Gateway. A customer gateway can be connected to multiple VPN Gateways.

3.  Create an IPsec connection

    An IPsec connection is a VPN channel established between a VPN Gateway and a customer gateway. The encrypted communication between the VPN Gateway and the on-premises data center can be achieved only after the IPsec connection is established.

4.  Configure the local gateway

    You need to load the VPN Gateway configurations to the local gateway device. For more information, see [Local CPE configurations](/intl.en-US/User Guide/Configure IPsec-VPN connections/Configure local gateways/Load the IPsec-VPN configuration to a Huawei firewall device.md).

5.  Configure the VPN Gateway route

    You need to configure a route in the VPN Gateway and publish it to the VPC route table. For more information, see [VPN Gateway route overview](/intl.en-US/User Guide/Manage a VPN Gateway/Configure routes of a VPN Gateway/VPN Gateway route overview.md).

6.  Test the connection

    Log on to an ECS instance \(without a public IP address\) in the connected VPC. ping the private IP address of a server in the on-premises data center to check whether the connection is established.


For more information, see [t13351.md\#](/intl.en-US/IPsec-VPN Quick Start/Connect on-premises data centers to VPC networks.md).

