# Load the IPsec-VPN configuration to a Cisco firewall device

When you use IPsec-VPN to establish a site-to-site connection, you must load the IPsec-VPN configuration to the gateway device that is deployed in the data center after you configure the VPN gateway on Alibaba Cloud. This topic provides an example on how to load the IPsec-VPN configuration to a Cisco firewall device that is deployed in a data center.

The following table describes the network configurations of the virtual private cloud \(VPC\) and the data center in this example.

|Parameter|Example|
|:--------|:------|
|VPC|CIDR blocks of the vSwitches|192.168.10.0/24 and 192.168.11.0/24|
|Public IP address of the VPN gateway|47.XX.XX.161|
|Data center|Private CIDR block|10.10.10.0/24|
|Public IP address of the Cisco firewall device|124.XX.XX.171|

**Note:** If you want to connect multiple CIDR blocks of a data center to a VPC, we recommend that you create an equivalent number of IPsec-VPN connections and add routes to the VPN gateway on Alibaba Cloud.

## Configure IKEv1 VPN

Prerequisites:

-   An IPsec-VPN connection is created in a VPC on Alibaba Cloud. For more information, see [Create an IPsec-VPN connection](/intl.en-US/User Guide/Configure IPsec-VPN connections/Manage an IPsec-VPN connection/Create an IPsec-VPN connection.md).

-   The configuration of the IPsec-VPN connection is downloaded. For more information, see [Download the configuration file of an IPsec-VPN connection](/intl.en-US/User Guide/Configure IPsec-VPN connections/Manage an IPsec-VPN connection/Download the configuration of an IPsec-VPN connection.md). The following configuration is used in this example.

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


1.  Log on to the command-line interface of the firewall device.

2.  Create an ISAKMP policy.

    ```
    crypto isakmp policy 1 
    authentication pre-share 
    encryption aes
    hash sha 
    group  2
    lifetime 86400
    ```

3.  Set the pre-shared key.

    ```
    crypto isakmp key 123456 address 47.XX.XX.161
    ```

4.  Specify the IPsec protocol.

    ```
    crypto ipsec transform-set ipsecpro64 esp-aes esp-sha-hmac 
    mode tunnel
    ```

5.  Create network access control lists \(ACLs\) to specify the inbound and outbound traffic flows to be encrypted.

    **Note:** If multiple CIDR blocks are configured on the firewall device, you must create a network ACL for each CIDR block.

    ```
    access-list 100 permit ip 10.10.10.0 0.0.0.255 192.168.10.0 0.0.0.255
    access-list 100 permit ip 10.10.10.0 0.0.0.255 192.168.11.0 0.0.0.255
    ```

6.  Create an IPsec policy.

    ```
    crypto map ipsecpro64 10 ipsec-isakmp
    set peer 47.XX.XX.161
    set transform-set ipsecpro64
    set pfs group2
    match address 100
    ```

7.  Apply the IPsec policy.

    ```
    interface g0/0
    crypto map ipsecpro64
    ```

8.  Configure static routes

    ```
    ip route 192.168.10.0 255.255.255.0 47.XX.XX.161
    ip route 192.168.11.0 255.255.255.0 47.XX.XX.161
    ```

9.  Test the connectivity.

    You can use a host on Alibaba Cloud and a host in the data center to test the connectivity.


## Configure IKEv2 VPN

Prerequisites:

-   An IPsec-VPN connection is created in a VPC on Alibaba Cloud. For more information, see [Create an IPsec-VPN connection](/intl.en-US/User Guide/Configure IPsec-VPN connections/Manage an IPsec-VPN connection/Create an IPsec-VPN connection.md).

-   The configuration of the IPsec-VPN connection is downloaded. For more information, see [Download the configuration file of an IPsec-VPN connection](/intl.en-US/User Guide/Configure IPsec-VPN connections/Manage an IPsec-VPN connection/Download the configuration of an IPsec-VPN connection.md). The following configuration is used in this example.

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


1.  Log on to the command-line interface of the firewall device.

2.  Specify the algorithm that is used in IKE Phase 1 negotiations.

    ```
    crypto ikev2 proposal daemon 
    encryption aes-cbc-128
    integrity sha1
    group 2
    ```

3.  Create an IKEv2 policy and set an IKEv2 proposal.

    ```
    crypto ikev2 policy ipsecpro64_v2
    proposal daemon
    ```

4.  Set the pre-shared key.

    ```
    crypto ikev2 keyring ipsecpro64_v2 
    peer vpngw 
    address 47.XX.XX.161
    pre-shared-key 0 123456
    ```

5.  Configure identity verification.

    ```
    crypto ikev2 profile ipsecpro64_v2
    match identity remote address 47.XX.XX.161 255.255.255.255
    identity local address 10.10.10.1 
    authentication remote pre-share     
    authentication local pre-share 
    keyring local ipsecpro64_v2
    ```

6.  Specify the IPsec protocol.

    ```
    crypto ipsec transform-set ipsecpro64_v2 esp-aes esp-sha-hmac
    mode tunnel
    ```

7.  Create network ACLs to specify the inbound and outbound traffic flows to be encrypted.

    **Note:** If multiple CIDR blocks are configured on the firewall device, you must create a network ACL for each CIDR block.

    ```
    access-list 100 permit ip 10.10.10.0 0.0.0.255 192.168.10.0 0.0.0.255
    access-list 100 permit ip 10.10.10.0 0.0.0.255 192.168.11.0 0.0.0.255
    ```

8.  Create an IPsec policy.

    ```
    crypto map ipsecpro64_v2 10 ipsec-isakmp
    set peer 47.XX.XX.161
    set transform-set ipsecpro64_v2 
    set pfs group2
    set ikev2-profile ipsecpro64_v2
    match address 100
    ```

9.  Apply the IPsec policy.

    ```
    interface g0/1
    crypto map ipsecpro64_v2
    ```

10. Configure static routes

    ```
    ip route 192.168.10.0 255.255.255.0 47.XX.XX.161
    ip route 192.168.11.0 255.255.255.0 47.XX.XX.161
    ```

11. Test the connectivity.

    You can use a host on Alibaba Cloud and a host in the data center to test the connectivity.


