# Add a policy-based route entry

This topic describes how to add a policy-based route entry after an IPsec-VPN connection is created. Policy-based routing \(PBR\) is a technique that routes packets based on source and destination IP addresses.

1.  Log on to the [VPN gateway console](https://vpc.console.aliyun.com/vpn).

2.  In the left-side navigation pane, choose **VPN** \> **VPN Gateways**.

3.  Select the region where the VPN gateway is deployed.

4.  On the **VPN Gateways** page, find the target VPN gateway and click the instance ID in the **Instance ID/Name** column.

5.  Click the **Policy-based Routing** tab, and then click **Add Route Entry**.

6.  In the **Add Route Entry** dialog box, set the following parameters and click **OK**.

    |Parameter|Description|
    |:--------|:----------|
    |**Destination CIDR Block**|The CIDR block that you want to access.|
    |**Source CIDR Block**|The CIDR block of the VPC network.|
    |**Next Hop Type**|Select IPsec Connection.|
    |**Next Hop**|Select an IPsec instance to create an IPsec-VPN connection.|
    |**Publish to VPC**|Specify whether to automatically publish new route entries to the VPC route table.     -   Yes \(Recommended\): automatically publishes new route entries to the VPC route table.
    -   No: does not automatically publish new route entries to the VPC route table.
 **Note:** If you select No, you must manually publish new route entries to the VPC route table. |
    |**Weight**|Select a weight. Valid values:     -   100: indicates that the priority of the route entry is high.
    -   0: indicates that the priority of the route entry is low.
 **Note:** If two policy-based route entries are configured with the same destination CIDR block, you cannot set the weights of both route entries to 100. |


