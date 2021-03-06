# 建立VPC到本地数据中心的连接

本文介绍如何使用IPsec-VPN建立专有网络（VPC）到本地数据中心的VPN连接，从而实现本地数据中心与VPC的互通。

开始前，请确保满足以下条件：

-   您已经注册了阿里云账号。如未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm)。
-   检查本地数据中心的网关设备。阿里云VPN网关支持标准的IKEv1和IKEv2协议。因此，只要支持这两种协议的设备都可以和云上VPN网关互连，例如华为、华三、山石、深信服、Cisco ASA、Juniper、SonicWall、Nokia、IBM和Ixia等厂商的设备。
-   本地数据中心的网关已经配置了静态公网IP。
-   本地数据中心的网段和VPC的网段不能重叠。

某公司在阿里云创建了VPC，网段为192.168.0.0/16。本地数据中心的网段为172.16.0.0/12，本地VPN设备的公网IP为211.xx.xx.68。因公司业务发展，需要本地数据中心与云上VPC互通。

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6649549951/p3312.png)

如上图，您可以通过IPsec-VPN，建立本地数据中心与云上VPC的连接，实现云上和云下的互通。

## 步骤一：创建VPN网关

完成以下操作，创建VPN网关。

1.  登录[VPN网关管理控制台](https://vpc.console.aliyun.com/vpn)。

2.  在左侧导航栏，单击**VPN** \> **VPN网关**。

3.  在**VPN网关**页面，单击**创建VPN网关**。

4.  在购买页面，根据以下信息配置VPN网关，然后单击**立即购买**并完成支付。

    -   **实例名称**：输入VPN网关的实例名称。
    -   **地域和可用区**：选择VPN网关的地域和可用区。

        **说明：** 确保VPC的地域和VPN网关的地域相同。

    -   **VPC**：选择要连接的VPC。
    -   **带宽规格**：选择一个带宽规格。带宽规格是VPN网关所具备的公网带宽。
    -   **IPsec-VPN**：选择开启IPsec-VPN功能。
    -   **SSL-VPN**：选择是否开启SSL-VPN功能。SSL-VPN功能允许您从任何位置的单台计算机连接到专有网络。
    -   **SSL连接数**： 选择您需要同时连接的客户端最大规格。

        **说明：** 本选项只有在选择开启了SSL-VPN功能后才可配置。

    -   **计费周期**：选择购买时长。
5.  返回VPN网关页面，查看创建的VPN网关。

    刚创建好的VPN网关的状态是准备中，约两分钟左右会变成正常状态。正常状态表明VPN网关完成了初始化，可以正常使用了。

    **说明：** VPN网关的创建一般需要1~5分钟。


## 步骤二：创建用户网关

完成以下操作，创建用户网关。

1.  在左侧导航栏，单击**VPN** \> **用户网关**。

2.  选择用户网关的地域。

3.  在用户网关页面，单击**创建用户网关**。

4.  在创建用户网关对话框，根据以下信息配置用户网关，然后单击**确定**。

    -   **名称**：输入用户网关的名称。
    -   **IP地址**：输入VPC要连接的本地数据中心网关设备的公网IP。本示例输入**211.xx.xx.68**。
    -   **描述**：输入用户网关的描述信息。

## 步骤三：创建IPsec连接

完成以下操作，创建IPsec连接。

1.  在左侧导航栏，单击**VPN** \> **IPsec连接**。

2.  选择创建IPsec连接的地域。

3.  在IPsec连接页面，单击**创建IPsec连接**。

4.  在创建IPsec连接页面，根据以下信息配置IPsec连接，然后单击**确定**。

    -   **名称**：输入IPsec连接的名称。
    -   **VPN网关**：选择已创建的VPN网关。
    -   **用户网关**：选择要连接的用户网关。
    -   **本端网段**：输入已选VPN网关所属VPC的网段。本示例输入**192.168.0.0/16**。
    -   **对端网段**：输入本地数据中心的网段。本示例输入**172.16.0.0/12**。
    -   **立即生效**：选择是否立即生效。
        -   **是**：配置完成后立即进行协商。
        -   **否**：当有流量进入时进行协商。
    -   **预共享密钥**：输入共享密钥，该值必须与本地网关设备的预共享密钥一致。

        其他选项使用默认配置。


## 步骤四：在本地网关设备中加载VPN配置

完成以下操作，在本地网关设备中加载VPN配置。

1.  在左侧导航栏，单击**VPN** \> **IPsec连接**。

2.  选择IPsec连接的地域。

3.  在IPsec连接页面，找到目标IPsec连接，然后单击**操作**列下的**更多操作** \> **下载对端配置**。

4.  根据本地网关设备的配置要求，将下载的配置添加到本地网关设备中。详细信息，请参见[本地网关配置](/cn.zh-CN/用户指南/配置IPsec-VPN/本地网关配置/华为防火墙配置.md)。

    下载配置中的RemotSubnet和LocalSubnet与创建IPsec连接时的本端网段和对端网段是相反的。因为从阿里云VPN网关的角度看，对端是用户IDC的网段，本端是VPC网段；而从本地网关设备的角度看，LocalSubnet就是指本地IDC的网段，RemotSubnet则是指阿里云VPC的网段。


## 步骤五：配置VPN网关路由

完成以下操作，配置VPN网关路由。

1.  在左侧导航栏，单击**VPN** \> **VPN网关**。

2.  选择VPN网关的地域。

3.  在VPN网关页面，找到目标VPN网关，单击实例ID/名称列下的实例ID。

4.  在目的路由表页签，单击**添加路由条目**。

5.  在添加路由条目对话框，根据以下信息配置目的路由，然后单击**确定**。

    -   **目标网段**：输入本地IDC侧的私网网段。本示例输入**172.16.0.0/12**。
    -   **下一跳类型**：选择IPsec连接。
    -   **下一跳**：选择IPsec连接实例。
    -   **发布到VPC**：选择是否将新添加的路由发布到VPC路由表。本示例选择**是**。
    -   **权重**：选择权重值。本示例选择**100**。

## 步骤六：测试访问

登录到阿里云VPC内一台无公网IP的ECS实例，并通过ping命令ping本地数据中心内一台服务器的私网IP地址，验证通信是否正常。

