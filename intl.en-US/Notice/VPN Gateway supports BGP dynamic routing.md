# VPN Gateway supports BGP dynamic routing

VPN Gateway supports the dynamic routing feature of Border Gateway Protocol \(BGP\). You can use a VPN gateway to connect a data center to Alibaba Cloud. Then, you can enable BGP dynamic routing for the VPN gateway to automatically learn routes. This reduces the costs of network maintenance and avoids network configuration errors.

**Note:** The BGP dynamic routing feature is available for only users that are included in the whitelist. If you are not included in the whitelist but want to use the feature,[submit a ticket](https://workorder-intl.console.aliyun.com/?spm=5176.2020520001.nav-right.dticket.59b44bd3QY32s9#/ticket/createIndex).

## Overview

BGP is a dynamic routing protocol based on Transmission Control Protocol \(TCP\). BGP is used to exchange routing and network accessibility information across autonomous systems \(AS\).

BGP dynamic routing is developed from the IPsec-VPN feature. BGP dynamic routing integrates the route learning and route advertisement features of Cloud Enterprise Network \(CEN\). You can establish a connection between Alibaba Cloud and your data center in a more efficient, flexible, and reliable manner with BGP dynamic routing.

BGP dynamic routing provides the following features:

-   Automatically advertises dynamic routes to the cloud and data centers, and handles route conflicts.
-   Enables static routing and dynamic routing. These routing methods allows you to route network traffic from specified egresses.
-   Establishes multiple tunnel connections between a VPN gateway and a data center. Supports equal-cost multi-path routing \(ECMP\) to achieve disaster recovery.

**Note:** Before you use BGP dynamic routing to establish a VPN connection, take note of the following items:

-   Make sure that the same autonomous system number \(ASN\) of the data center is specified on the virtual border router \(VBR\) and the VPN gateway. This condition must be met when you connect the data center to a virtual private cloud \(VPC\) by using leased lines and VPN gateways for connection resilience. This avoids route flapping in the data center.
-   If multiple VPCs are associated with the same CEN instance, make sure that the VPN gateways associated with the VPCs are not connected to the data centers through BGP. This avoids route flapping in the CEN.
-   If you use the same VPN gateway to establish VPN connections with more than one data center, you must not advertise routes of different VPN connections to each other.
-   If multiple VPN gateways are created in a VPC, you must not advertise routes of different VPN gateways to each other.

## How dynamic routes are advertised

After a VPN connection is established on a VPN gateway, dynamic routes are advertised in the following ways:

-   To Alibaba Cloud

    The customer VPN gateway automatically learns BGP routes that are destined for the CIDR block of the data center and advertises the routes to the VPN gateway in the cloud. If you enable automatic BGP advertisement for the VPN gateway on Alibaba Cloud, the VPN gateway uses BGP to learn routes and automatically advertises the routes to the default route table of the VPC. No BGP route is advertised to the custom route tables.

-   To the data center

    The VPN gateway on Alibaba Cloud automatically learns BGP routes from the default route table of the VPC, and then advertises the routes to the customer VPN gateway.


## Routing priorities

The following table shows how routes of different types are applied when routes in the route table of a VPN gateway or a VPC conflict with each other.

**Note:** Different types of routes are applied in the following order: P0 \> P1 \> P2 \> P3.

|Route type|Priority of routes on a VPN gateway|Priority of routes within a VPC|
|----------|-----------------------------------|-------------------------------|
|Specific routes|P0|P0|
|Default routes|P1|P1|
|Static routing|P2|P2|
|Dynamic routing|P3|P3|

## Limits

Each VPN gateway can hold a BGP route table that contains at most 50 route entries. To increase the quota,[submit a ticket](https://workorder-intl.console.aliyun.com/?spm=5176.2020520001.nav-right.dticket.59b44bd3QY32s9#/ticket/createIndex).

## Use BGP dynamic routing

For more information, see [Establish a connection between a VPC network and an on-premises data center with BGP dynamic routing](/intl.en-US/IPsec-VPN Quick Start/Establish a connection between a VPC network and an on-premises data center with BGP dynamic routing.md).

