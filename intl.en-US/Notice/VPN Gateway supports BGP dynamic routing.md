# VPN Gateway supports BGP dynamic routing

VPN Gateway supports the dynamic routing feature of Border Gateway Protocol \(BGP\). You can use a VPN gateway to connect a on-premises data center to Alibaba Cloud. Then, you can enable BGP dynamic routing for the VPN gateway to automatically learn routes. This reduces the costs of network maintenance and helps avoid network configuration errors.

**Note:** The BGP dynamic routing feature is supported in all regions except China \(Heyuan\).

## Overview of BGP dynamic routing

BGP is a dynamic routing protocol based on Transmission Control Protocol \(TCP\). BGP is used to exchange routing and network accessibility information across Autonomous Systems.

BGP dynamic routing is developed from the IPsec-VPN feature. BGP dynamic routing integrates the route learning and route advertisement features of Cloud Enterprise Network \(CEN\). You can establish a connection between Alibaba Cloud and your on-premises data center in a more efficient, flexible, and reliable manner with BGP dynamic routing.

BGP dynamic routing provides the following functions:

-   Automatically advertises dynamic routes to the cloud and on-premises data centers, and handles route conflicts.
-   Enables static routing and dynamic routing. This allows you to route network traffic from specified egresses.
-   Supports equal-cost multi-path routing \(ECMP\). You can create a multi-path connection between a VPN gateway and an on-premises data center to achieve disaster recovery for high availability.

**Note:** Before you use BGP dynamic routing to establish a VPN connection, note the following issues:

-   Make sure that the same Autonomous System Number \(ASN\) of the on-premises data center is specified on the virtual border router \(VBR\) and the VPN gateway. This condition must be met when you connect the on-premises data center to a virtual private cloud \(VPC\) by using leased lines and VPN gateways for connection resilience. This avoids route flapping in the on-premises data center.
-   If multiple VPCs are associated with the same CEN instance, make sure that the VPN gateways associated with the VPCs are not connected to the on-premises data centers through BGP. This avoids route flapping in the CEN.
-   If you use the same VPN gateway to establish VPN connections with more than one on-premises data center, you must not import routes of different route tables to each other.
-   If multiple VPN gateways are created for a VPC, you must not import routes of different VPN gateways to each other.

## How dynamic routes are advertised

After a VPN connection is established on a VPN gateway, dynamic routes are advertised in the following ways:

-   To Alibaba Cloud

    The customer VPN gateway automatically learns BGP routes that are destined for the CIDR block of the on-premises data center and advertises the routes to the VPN gateway on the cloud. If you enable automatic BGP propagation for the VPN gateway on Alibaba Cloud, the VPN gateway uses BGP to learn routes and automatically propagates the routes to the default route table of the VPC. No BGP route is propagated to the custom route tables.

-   To the on-premises data center

    The VPN gateway on Alibaba Cloud automatically learns BGP routes from the default route table of the VPC, and then advertises the routes to the customer VPN gateway.


## Routing priorities

The following table shows how routes of different types are applied when routes in the route table of a VPN gateway or a VPC conflict with each other.

**Note:** Different types of routes are applied in the following order: P0 \> P1 \> P2 \> P3.

|Route type|Priority of routes on a VPN gateway|Priority of routes within a VPC|
|----------|-----------------------------------|-------------------------------|
|Specific routes|P0|P0|
|Default routes|P1|P1|
|Static routes|P2|P2|
|Dynamic routes|P3|P3|

## Limits

Each VPN gateway can hold a BGP route table that contains up to 50 route entries. To increase the quota,[submit a ticket](https://workorder-intl.console.aliyun.com/?spm=5176.2020520001.nav-right.dticket.59b44bd3QY32s9#/ticket/createIndex).

## Use BGP dynamic routing

For more information about how to use BGP dynamic routing to connect a VPC to an on-premises data center, see [Establish a connection between a VPC network and an on-premises data center with BGP dynamic routing](/intl.en-US/IPsec-VPN Quick Start/Establish a connection between a VPC network and an on-premises data center with BGP dynamic routing.md).

