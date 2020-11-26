# Load the IPsec-VPN configuration to a Huawei firewall device

After you configure an IPsec-VPN connection on Alibaba Cloud, you must load the configuration of the IPsec-VPN connection to the gateway device deployed in the on-premises data center.

Alibaba Cloud VPN gateways support the standard IKEv1 and IKEv2 protocols. Gateway devices that support these two protocols can connect to VPN gateways on Alibaba Cloud, such as gateway devices from Huawei, H3C, Hillstone, Sangfor, Cisco ASA, Juniper, SonicWall, Nokia, IBM, and Ixia.

The example in this topic demonstrates how to load the IPsec-VPN configuration to a Huawei firewall device deployed in an on-premises data center.

|Parameter|Example|
|:--------|:------|
|VPC|CIDR blocks of the VSwitches|192.168.10.0/24 and 192.168.11.0/24|
|Public IP address of the VPN gateway|47.xx.xx.10|
|On-premises data center|Private CIDR block|10.10.10.0/24|
|Public IP address of the firewall|124.xx.xx.215/26|
|Outbound port \(external\)|10GE1/0/0|
|Inbound port \(internal\)|10GE1/0/1|

**Note:** If you want to connect multiple CIDR blocks of the on-premises data center to a virtual private cloud \(VPC\), we recommend that you create an equivalent number of IPsec-VPN connections and add routes on Alibaba Cloud. This way, each CIDR block of the on-premises data center can be connected to a VPC CIDR block.

## Configure IKEv1 VPN

**Prerequisites**

-   An IPsec-VPN connection is created in a VPC on Alibaba Cloud. For more information, see [t13359.md\#](/intl.en-US/User Guide/Configure IPsec-VPN connections/Manage an IPsec-VPN connection/Create an IPsec-VPN connection.md).

-   The configuration of the IPsec-VPN connection is downloaded.The configuration in the following table is used in this example.

|Protocol|Parameter|Example|
|:-------|:--------|:------|
|IKE|Authentication algorithm|SHA-1|
|Encryption algorithm|AES-128|
|DH group|group 2|
|IKE version|IKE v1|
|Lifecycle|86400|
|Negotiation mode|main|
|PSK|123456|
|IPsec|Authentication algorithm|SHA-1|
|Encryption algorithm|AES-128|
|DH group|group 2|
|IKE version|IKE v1|
|Lifecycle|86400|
|Negotiation mode|esp|


**Procedure**

Perform the following operations to load the configuration of the customer gateway to the Huawei firewall device:

1.  Go to the Huawei firewall management page, choose **Network** \> **Interface** \> **Interface List**. Add the outbound port 10GE1/0/0 to the **untrust** security zone and set the public IP address. Add the inbound port 10GE1/0/1 to the trust security zone and set the private IP address.
2.  Choose **Policy** \> **Security Policy** \> **New** to create a security policy.
3.  Choose **Network** \> **IPsec** \> **IPsec Policy List** \> **Add**, and configure the gateway device based on the following information:
    -   **Local Interface**: Select the outbound port. In this example, 10GE1/0/0 is selected.

    -   **Peer Address**: Enter the public IP address of the VPN gateway on Alibaba Cloud. In this example, 47.xx.xx.10 is entered.

    -   The pre-shared key must be the same as that used at the Alibaba Cloud side. In this example, 123456 is entered.

4.  On the Data Flow to Be Encrypted page, click **Add**. Add the data flow to be encrypted for all VSwitch CIDR blocks in the VPC based on the following information:
    -   **Source Address/Address-Set**: Enter the private CIDR block of the on-premises data center. In this example, 10.10.10.0/24 is entered.

    -   **Destination Address/Address-Set**: Enter the CIDR blocks of the VSwitches that are deployed in the VPC on Alibaba Cloud. In this example, 192.168.10.0/24 and 192.168.11.0/24 are entered.

5.  On the IKE/IPSec Protocol page, click **Advanced**. Configure the IKE protocol parameters based on the IPsec-VPN configuration that you downloaded.
6.  On the IPsec Parameters page, configure the IPsec protocol parameters based on the IPsec configuration that you downloaded.
7.  Choose **Network** \> **Route** \> **Static Route** \> **Static Route List** \> **Add** to configure static routes for the firewall. When you add a default route, the next hop is the public IP address of the firewall. When you add a route that points to the VPC on Alibaba Could, the next hop is the public IP address of the VPN gateway in the VPC.

## Configure IKEv2 VPN

**Prerequisites**

-   An IPsec-VPN connection is created in a VPC on Alibaba Cloud.

-   The configuration of the IPsec-VPN connection is downloaded. The configuration in the following table is used in this example.

    |Protocol|Parameter|Example|
    |:-------|:--------|:------|
    |IKE|Authentication algorithm|SHA-1|
    |Encryption algorithm|AES-128|
    |DH group|group 2|
    |IKE version|IKE v2|
    |Lifecycle|86400|
    |PRF algorithm|SHA-1|
    |PSK|123456|
    |IPsec|Authentication algorithm|SHA-1|
    |Encryption algorithm|AES-128|
    |DH group|group 2|
    |IKE version|IKE v2|
    |Lifecycle|86400|
    |Negotiation mode|esp|


## Procedure

Perform the following operations to load the configuration of the customer gateway to the Huawei firewall device.

1.  Go to the Huawei firewall management page. Choose **Network** \> **Interface** \> **Interface List**. Add the outbound port 10GE1/0/0 to the **untrust** security zone and set the public IP address. Add the inbound port 10GE1/0/1 to the **trust** security zone and set the private IP address.
2.  Choose **Policy** \> **Security Policy** \> **Add** to create a security policy.
3.  Choose **Network** \> **IPsec** \> **IPsec Policy List** \> **Add**, and configure the gateway device based on the following information:
    -   **Local Interface**: Select the firewall outbound port. In this example, 10GE1/0/0 is selected.

    -   **Peer Address**: Enter the public IP address of the VPN gateway on Alibaba Cloud. In this example, 47.xx.xx.10 is entered.

    -   The pre-shared key must be the same as that used at the Alibaba Cloud side. In this example, 123456 is entered.

4.  On the Data Flow to Be Encrypted page, click **Add**. Add the data flow to be encrypted for all VSwitch CIDR blocks in the VPC based on the following information:
    -   **Source Address/Address-Set**: Enter the private CIDR block of the on-premises data center. In this example, 10.10.10.0/24 is entered.

    -   **Destination Address/Address-Set**: Enter the CIDR blocks of the VSwitches in the VPC. In this example, 192.168.10.0/24 and 192.168.11.0/24 are entered.

5.  On the IKE/IPSec Protocol page, click **Advanced**. Configure the IKE parameters based on the IPsec-VPN configuration that you downloaded.
6.  On the IPsec Parameters page, configure the IPsec protocol parameters based on the IPsec-VPN connection that you downloaded.
7.  Choose **Network** \> **Route** \> **Static Route** \> **Static Route List** \> **Add** to configure static routes for the firewall. When you add a default route, the next hop is the public IP address of the firewall. When you add a route that points to a VPC, the next hop is the public IP address of the VPN gateway.

