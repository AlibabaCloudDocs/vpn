# FAQ about IPsec-VPN connections

## 1. What can I do if the state of an IPsec-VPN connection indicates "Phase 1 negotiations failed"?

When the configuration of the VPN gateway on Alibaba Cloud is different from that of the on-premises VPN gateway, Phase 1 negotiations may fail. The following table describes the possible causes and solutions.

|Cause|Solution|Log|
|-----|--------|---|
|The pre-shared keys are different.|Configure the same pre-shared key on both VPN gateways.|```
invalid HASH_V1 payload length, decryption failed?
could not decrypt payloads
message parsing failed
``` |
|The IKE protocol versions are different.|Configure the same IKE version. For example, you can set the IKE protocol version to IKEv1 or IKEv2 on both VPN gateways of the IPsec-VPN connection.|```
parsed IKE_SA_INIT response 0 [ N(NO_PROP) ]
received NO_PROPOSAL_CHOSEN notify error
received AUTHENTICATION_FAILED error notify
``` |
|The negotiation modes are different.|Configure the same negotiation mode. For example, you can set the negotiation mode to main or aggressive on both VPN gateways of the IPsec-VPN connection.|```
received AUTHENTICATION_FAILED error notifyed
``` |
|The values of LocalId or RemoteId are different.|Set the same value for LocalId or RemoteId on both VPN gateways.|```
[IKE] IDir xxxx does not match to xxxx
``` |
|The encryption or authentication algorithms are different.|Configure the same encryption and authentication algorithms on both VPN gateways.|N/A|
|The DH groups are different.|Configure the same DH group. For example, you can set the DH group to group 2 on both VPN gateways of the IPsec-VPN connection.|N/A|
|The peering VPN gateway does not respond.|Make sure that the peering VPN gateway functions as expected.|```
[IKE] sending retransmit 1 of request message ID 0, seq 1
``` |
|A wrong public IP address is specified when you create the customer VPN gateway.|You must specify the public IP address of the on-premises VPN gateway when you create the customer gateway.|```
received UNSUPPORTED_CRITICAL_PAYLOAD error notify
``` |

In some scenarios, the state of the IPsec-VPN connection indicates "Phase 1 negotiations failed" even if the preceding configurations on both VPN gateways are the same. To resolve this problem, we recommend that you change the negotiation mode to aggressive.

## 2. What can I do if the state of an IPsec-VPN connection indicates “Phase 2 negotiations failed”?

The following table describes the possible causes and solutions.

|Cause|Solution|Log|
|-----|--------|---|
|The interesting traffic flows are different.|Check the private CIDR blocks of both VPN gateways of the IPsec-VPN connection. Make sure that the private CIDR blocks are set correctly.|-   Main mode

    ```
received INVALID_ID_INFORMATION error notify
    ```

-   Aggressive mode

    ```
received HASH payload does not match 
integrity check failed
    ``` |
|The encryption or authentication algorithms are different.|Configure the same encryption and authentication algorithms on both VPN gateways of the IPsec-VPN connection.|```
parsed INFORMATIONAL_V1 request xxxx [ HASH N(NO_PROP) ]
received NO_PROPOSAL_CHOSEN error notify
``` |
|The DH groups are different.|Configure the same DH group on both VPN gateways of the IPsec-VPN connection.|```
ESP:AES_CBC_256/HMAC_SHA1_96/MODP_1024/NO_EXT_SEQ
ESP:AES_CBC_128/HMAC_SHA1_96/MODP_1024/NO_EXT_SEQ, 
ESP:AES_CBC_128/AES_CBC_192/AES_CBC_256/3DES_CBC/BLOWFISH_CBC_256/HMAC_SHA2_256_128/HMAC_SHA2_384_192/HMAC_SHA2_512_256/HMAC_SHA1_96/AES_XCBC_96/HMAC_MD5_96/NO_EXT_SEQ
no matching proposal found, sending NO_PROPOSAL_CHOSEN
``` |

## 3. What can I do if the state of an IPsec-VPN connection indicates “Phase 2 negotiations succeeded”, but the Elastic Compute Service \(ECS\) instances in the virtual private cloud \(VPC\) cannot access the servers in the on-premises data center?

If public IP addresses are used as private IP addresses within the on-premises data center and the ECS instances can access the Internet, submit a ticket to modify the configuration. Otherwise, check the routes and other relevant configurations based on the following information:

-   Check the routes on the router of the VPC.

-   Check the configuration of the firewall or iptables in the on-premises data center. Make sure that requests sent from the private CIDR block of the VPC are allowed to reach the on-premises data center.


## 4. What can I do if the state of an IPsec-VPN connection indicates “Phase 2 negotiations succeeded”, but servers in the on-premises data center cannot access the ECS instances in the VPC?

Check the configurations based on the following information:

-   Check the routes and ACLs in the on-premises data center. Make sure that data is allowed to be transmitted to the VPC through the IPsec-VPN connection.
-   Check the rules in the security group of the ECS instances. Make sure that requests from the private CIDR block of the on-premises data center are allowed to reach the ECS instances.

## 5. What can I do if the state of the IPsec-VPN connection indicates “Phase 2 negotiations succeeded”, but communication is successful only in some of the CIDR blocks?

Check whether the IKEv2 protocol is used. If you want to establish an IPsec-VPN connection to connect multiple CIDR blocks, we recommend that you use the IKEv2 protocol.

If the IKEv2 protocol is used, check the Security Association \(SA\) on the on-premises VPN gateway. In most cases, only one SA is created for each IPsec-VPN connection, for example, 172.30.96.0/19 === 10.0.0.0/8 172.30.128.0/17.

If more than one SA exists, it indicates that the IKEv2 protocol that the on-premises VPN gateway uses is not a standard protocol. To resolve this problem, you must create multiple IPsec-VPN connections to connect the CIDR blocks. For example, you can split the IPsec-VPN connection 172.30.96.0/19 <=\> 10.0.0.0/8 172.30.128.0/17 into IPsec-VPN connection A 172.30.96.0/19 <=\> 10.0.0.0/8 and IPsec-VPN connection B 172.30.96.0/19 <=\> 172.30.128.0/17.

**Note:** The two IPsec-VPN connections must share the Phase 1 SA. Make sure that the same Phase 1 negotiation settings are configured for the IPsec-VPN connections.

## 6. What can I do if the state of the IPsec-VPN connection indicates “Phase 2 negotiations succeeded”, but the on-premises data center cannot access the ECS instances in the VPC?

**Cause**: A Huawei firewall device is used as the gateway device, and nat enable is set on the outbound port. As a result, the source IP addresses of all packets from the outbound port are converted to the IP address of the outbound port.

**Solution**:

1.  Run the `nat disable` command to disable the NAT feature on the outbound port.
2.  Configure NAT policies.

    ```
    nat-policy interzone trust untrust outbound
    policy 0
    action no-nat
    policy source 192.168.0.0 mask 24
    policy destination 192.168.1.0 mask 24
    policy 1 
    action source-nat
    policy source 192.168.0.0 mask 24
    easy-ip Dialer0
    ```

    Where:

    192.168.0.0 is the private CIDR block of the on-premises VPN gateway.

    192.168.1.0 is the private CIDR block of the VPN gateway that is created for the VPC.

    Dialer0 is the outbound port of the on-premises VPN gateway.


