# 通过LDAP认证建立SSL-VPN连接

本文为您介绍如何通过应用身份服务IDaaS（Alibaba Cloud Identity as a Service）LDAP认证建立SSL-VPN连接。

某公司在美国（硅谷）地域创建了VPC，网段为192.168.0.0/16。因业务发展，出差员工需要使用客户端访问云上VPC资源。

![LDAP认证架构图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1336294161/p244121.png)

该公司拥有自己的AD（Active Directory）系统，为安全起见，公司希望出差的员工可以在通过公司AD系统的身份认证后，再访问云上的VPC资源。

如上图，您可以在云上创建VPN网关，配置SSL服务端并开启双因子认证，指定IDaaS实例进行LDAP认证。在员工通过SSL-VPN登录时，需要先到IDaaS系统中进行LDAP认证，LDAP认证会将员工的用户名和密码发送到公司的AD系统中去进行验证，并返回验证结果。只有在员工输入的账户信息验证通过后，VPN网关才会帮员工建立SSL-VPN连接，进而允许其访问云上VPC资源。

## 准备工作

在您执行以下操作前，请确保您已经满足以下条件：

-   您已经购买了标准版IDaaS实例。具体操作，请参见[开通和试用流程](https://help.aliyun.com/document_detail/178746.html?spm=5176.b73997031.0.dexternal.21c67508cbam7i)。

    本文示例中，已在新加坡地域购买了标准版IDaaS实例。

-   您已经创建了专有网络VPC（Virtual Private Cloud）。更多信息，请参见[使用专有网络](/cn.zh-CN/专有网络和交换机/使用专有网络.md)。

    本文示例中，已在美国（硅谷）地域创建了VPC，VPC的网段为192.168.0.0/16。其中，ECS使用网段为192.168.0.0/24。

-   您已知您AD系统所在服务器（本文也称作LDAP服务器）的公网IP地址和服务端口。

    本文示例中，AD系统部署在Windows Server 2019系统中，其公网IP地址为47.XX.XX.8，服务端口为389。

-   您已知您LDAP服务器的Base DN。

    本文示例中，LDAP服务器的Base DN为dc=zxtest,dc=com。

-   您已知您LDAP服务器管理员的DN、用户名和密码。

    本文示例中，管理员账户名为Administrator，密码为1\*\*\*\*2。其DN为cn=Administrator,cn=Users,dc=zxtest,dc=com，如下图所示。

    ![管理员DN](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4951564161/p244831.png)


## 配置步骤

![LDAP配置步骤](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7434284161/p244732.png)

## 步骤一：开启LDAP认证

在您建立SSL-VPN连接前，您需要在IDaaS实例中开启LDAP认证功能并同步账户数据，用于后续的身份验证。

1.  添加LDAP认证源。

    1.  [登录IDaaS管理控制台。](https://yundun.console.aliyun.com/?spm=5176.12818093.ProductAndService--ali--widget-home-product-recent.dre3.5adc16d0nYkX7a&p=idaas#/instanceList/cn-hangzhou)。

    2.  在左侧导航栏，单击**EIAM实例列表**。

    3.  在实例列表页面，单击目标实例ID。

    4.  在左侧导航栏，单击**认证源**。

    5.  在认证源页面的右上角，单击**添加认证源**。

    6.  在添加认证源页面，找到LDAP图标![LDAP图标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9311954161/p244660.png)，单击**操作**列的**添加认证源**。

    7.  在**添加认证源（LDAP）**面板，配置LDAP服务器信息，然后单击**提交**。

        -   **认证源ID**：由系统自动生成。
        -   **认证源名称**：输入自定义名称。
        -   **LDAP URL**：LDAP服务器连接地址，LDAP服务器即指您部署AD系统的服务器。地址填写格式例如：ldap://127.0.0.1:389/。本示例输入ldap://47.XX.XX.8:389/。

            若主机的IP地址为IPv6地址格式，则地址需放在中括号（\[\]）内，例如：ldap://\[0000:0000:0000:0000:0000:0000:0001\]:389/。

            **说明：** IDaaS目前只支持公网访问，LDAP服务器需要提供公网地址，并开启389端口。您可以在您LDAP服务器的安全组策略中设置只允许IDaaS的公网IP可以访问LDAP服务器，关于IDaaS公网IP地址信息，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)至阿里云IDaaS团队咨询。

        -   **LDAP Base**：LDAP服务器Base DN。本示例输入dc=zxtest,dc=com。
        -   **LDAP账户**：LDAP服务器管理账户DN。本示例输入cn=Administrator,cn=Users,dc=zxtest,dc=com。
        -   **LDAP账户密码**：LDAP服务器管理账户密码。
        -   **过滤条件**：查询用户名的过滤条件。本示例输入\(sAMAccountName=$username$\)。

            具体匹配规则，请参见LDAP官方文档[LDAP Filters](https://ldap.com/ldap-filters/)。其中$username$为IDaaS系统用户名参数，为固定值。

        更多参数说明，请参见[LDAP认证登录](https://help.aliyun.com/document_detail/147473.html#topic566)。

    8.  在认证源页面，找到目标认证源，单击其**状态**列下的![启用](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6860784951/p97768.png)图标，然后在弹出的对话框中，单击**确定**，开启LDAP认证源。

2.  LDAP账户同步配置，将LDAP服务器中的账户数据导入到IDaaS系统中。

    1.  在左侧导航栏，单击**机构及组**。

    2.  在机构及组页面的右上角，单击**配置LDAP**。在**LDAP配置**面板，单击**新建配置**。

    3.  在**LDAP配置**面板的**服务器链接**页签下，配置以下信息，然后单击**保存**。

        -   **AD/LDAP名称**：输入自定义名称。
        -   **服务器地址**：输入您LDAP服务器的公网IP地址。本示例输入47.XX.XX.8。
        -   **端口号**：输入您LDAP服务器提供服务的端口号。本示例输入389。
        -   **Base DN**：输入要同步账户的节点DN。本示例输入dc=zxtest,dc=com。

            **说明：** 此项在添加完成后不可更改，因为在IDaaS系统与LDAP\(或AD\)服务器进行同步数据时，如果**Base DN**发生改变会使双方组织机构目录无法对应而导致数据同步失败，想要同步不同目录的数据建议添加多个LDAP配置来完成。

        -   **管理员DN**：请输入管理员账户DN。本示例输入cn=Administrator,cn=Users,dc=zxtest,dc=com。
        -   **密码**：输入管理员账户的密码。
        -   **类型选择**：选择您LDAP服务器的类型。本示例选择**Windows AD**。
        -   **所属OU节点**：账户数据导入IDaaS系统中组织机构的节点位置，若不选择，则导入到根OU下。本示例保持默认值。
        -   **LDAP同步至本系统**：启用该项后，可以手动从LDAP服务器同步数据到IDaaS系统。本示例选择**启用**。
        -   **本系统同步至LDAP**：启用该项后，可以从IDaaS系统同步数据到LDAP服务器。本示例选择**启用**。
        在您完成上述配置后，您可以单击**测试连接**来测试服务器的连通性。如果测试失败，请检查网络连通性，以及配置的连接参数是否正确。

    4.  在**LDAP配置**面板的**字段匹配规则**页签下，配置以下信息，然后单击**保存**。

        字段匹配规则为IDaaS系统的字段与LDAP服务器中属性的对应匹配规则，例如LDAP服务器中的cn字段对应为IDaaS系统中的用户名。

        -   **用户名**：本示例输入cn 。

            **说明：** 如果您AD系统中的账户的cn字段值为中文，则该账户无法拉取到IDaaS系统。建议您使用sAMAccountName字段。

        -   **外部ID**：Windows AD为objectGUID, OpenLdap为uid。本示例输入objectGUID 。
        -   **密码属性**：Windows AD为unicodePwd, OpenLdap为userPassword。本示例输入unicodePwd 。
        -   **用户唯一标识**：Windows AD为DistinguishedName, OpenLdap为EntryDN。本示例输入DistinguishedName 。
        -   **邮箱**：本示例输入mail 。
        更多信息，请参见[LDAP账户同步配置](https://help.aliyun.com/document_detail/151237.htm?spm=a2c4g.11186623.2.13.14436f84RPwfhZ#topic-2399816/section-wet-lo7-c6w)。

    5.  在机构及组页面，选择**导入** \> **LDAP** \> **组织结构**。

    6.  在**LDAP列表**面板，找到目标LDAP，单击**导入**，在弹出的对话框中，单击**确定**。在**组织机构临时数据**面板确认组织机构信息，单击**确定导入**。

    7.  在当前页面的**组织架构**区域，选择目标组织机构，在组织机构的详情区域，选择**导入** \> **LDAP** \> **账户**。

    8.  在**LDAP列表**面板，找到目标LDAP，单击**导入**，在弹出的对话框中，单击**确定**。在**账户临时数据LDAP列表**面板中确认账户信息，单击**确定导入**，实现LDAP服务器账户信息同步到IDaaS系统。

3.  开启云产品LDAP认证。

    1.  在左侧导航栏，选择**设置** \> **安全设置**。

    2.  在**安全设置**页面，单击**云产品AD认证**页签。

    3.  选择刚刚创建的LDAP认证源，启用该功能并单击**保存配置**。

        ![认证源](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6860784951/p97935.png)


## 步骤二：部署SSL-VPN

在开启LDAP认证后，您可以开始部署SSL-VPN，并开启SSL-VPN的双因子认证功能，关联已部署好的IDaaS实例，实现通过LDAP认证建立SSL-VPN连接。

1.  创建VPN网关。

    1.  登录[VPN网关管理控制台](https://vpc.console.aliyun.com/vpn)。

    2.  在左侧导航栏，选择**VPN** \> **VPN网关**。

    3.  在**VPN网关**页面，单击**创建VPN网关**。

    4.  在VPN网关的购买页面，根据以下信息配置VPN网关，然后单击**立即购买**完成支付。

        -   **实例名称**：输入VPN网关的实例名称。
        -   **地域和可用区**：选择VPN网关的地域。 本示例选择**美国（硅谷）**。

            **说明：** 确保已创建VPC的地域和VPN网关的地域相同。

        -   **网关类型**：选择要创建的VPN网关类型。本示例选择**普通型**。
        -   **VPC**： 选择要连接的VPC。
        -   **指定交换机**：是否指定VPN网关创建在VPC中的某一个交换机下。本示例选择**否**。

            如果您选择了**是**，您还需要指定具体的**虚拟交换机**。

        -   **带宽规格**：选择VPN网关的带宽规格，带宽规格是VPN网关所具备的公网带宽。本示例选择**10 Mbps**。
        -   **IPsec-VPN**： 选择开启或关闭IPsec-VPN功能，IPsec-VPN功能可以将本地数据中心与VPC或不同的VPC之间进行连接。本示例选择**关闭**。
        -   **SSL-VPN**： 选择开启或关闭SSL-VPN功能，SSL-VPN功能允许您从任何位置的单台计算机连接到VPC。本示例选择**开启**。
        -   **SSL连接数**： 选择您需要同时连接的客户端最大规格。 本示例选择**5**。

            **说明：** 本选项只有在选择开启了SSL-VPN功能后才可配置。

        -   **计费周期**：选择购买时长。
2.  创建SSL服务端。

    1.  在左侧导航栏，选择**VPN** \> **SSL服务端**。

    2.  在顶部状态栏处，选择SSL服务端的地域。

        本示例选择**美国（硅谷）**。

    3.  在**SSL服务端**页面，单击**创建SSL服务端**。

    4.  在**创建SSL服务端**面板，根据以下信息配置SSL服务端，然后单击**确定**。

        ![开启双因子认证](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8976654161/p88603.png)

        -   **名称**：输入SSL服务端的名称。

            长度为2~128个字符，以英文大小写字母或中文开头，可包含数字、下划线（\_）和短划线（-）。

        -   **VPN网关**：选择刚刚创建的VPN网关。
        -   **本端网段**：以CIDR地址块的形式输入客户端通过SSL-VPN连接要访问的网段。本示例输入**192.168.0.0/24**。
        -   **客户端网段**：以CIDR地址块的形式输入客户端连接服务端时使用的网段。本示例输入**10.0.0.0/24**。
        -   **高级配置**：打开高级配置，并完成以下配置。
            -   **协议**：选择SSL连接使用的协议，支持UDP和TCP。本示例使用默认配置**UDP**。
            -   **端口**：SSL连接使用的端口。本示例使用默认配置**1194**。
            -   **加密算法**：SSL连接使用的加密算法，支持AES-128-CBC、AES-192-CBC、AES-256-CBC。本示例使用默认配置**AES-128-CBC**。
            -   **是否压缩**：是否对传输数据进行压缩处理。本示例使用默认配置**否**。
            -   **双因子认证**：打开双因子认证，然后选择IDaaS实例。

                -   **IDaaS 实例所在地域**：IDaaS实例所在地域。本示例选择**新加坡**。
                -   **IDaaS实例**：选择目标IDaaS实例。
                **说明：** 如果您是首次使用双因子认证功能，请先完成授权后再创建SSL服务端。

3.  创建并下载SSL客户端证书。

    1.  在左侧导航栏，选择**VPN** \> **SSL客户端**。

    2.  在顶部状态栏处，选择SSL客户端的地域。

        本示例选择**美国（硅谷）**。

    3.  在**SSL客户端**页面，单击**创建SSL客户端证书**。

    4.  在**创建SSL客户端证书**面板，根据以下信息配置SSL客户端证书，然后单击**确定**。

        -   **名称**：输入SSL客户端证书的名称。

            长度为2~128个字符，以英文大小写字母或中文开头，可包含数字、下划线（\_）和短划线（-）。

        -   **SSL服务端**：选择刚刚创建的SSL服务端。
    5.  在**SSL客户端**页面，找到已创建的SSL客户端证书，然后单击**操作**列下的**下载**。

        SSL客户端证书会下载到您本地。


## 步骤三：配置客户端

完成以下操作，配置客户端。

1.  如果您使用的是Windows客户端，请参见以下步骤配置客户端。

    1.  下载并安装OpenVPN客户端。

        下载[OpenVPN](https://swupdate.openvpn.org/community/releases/openvpn-install-2.4.5-I601.exe)。

    2.  将已经下载的SSL客户端证书解压拷贝到OpenVPN\\config目录。

        本示例将证书解压拷贝到C:\\Program Files\\OpenVPN\\config目录，请您根据安装路径将证书解压拷贝到实际的目录。

        ![拷贝证书](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2023715161/p102364.png)

    3.  启动Openvpn客户端软件，并完成用户名和密码认证。

        ![LDAP客户端验证](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0953564161/p244849.png)

2.  如果您使用的是Linux客户端，请参见以下步骤配置客户端。

    1.  执行以下命令安装OpenVPN客户端。

        ```
        yum install -y openvpn
        ```

    2.  将已经下载的SSL客户端证书解压拷贝到/etc/openvpn/conf/目录。

    3.  执行以下命令启动OpenVPN客户端软件，并完成用户名密码验证。

        ```
        openvpn --config /etc/openvpn/conf/config.ovpn --daemon
        ```

        ![启动OpenVPN](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0528684951/p88600.png)

3.  如果您使用的是Mac客户端，请参见以下步骤配置客户端。

    1.  执行以下命令安装OpenVPN客户端。

        ```
        brew install openvpn
        ```

        **说明：** 如果尚未安装homebrew，请先安装homebrew。

    2.  执行以下命令删除默认配置文件。

        ```
        rm /usr/local/etc/openvpn/*
        ```

    3.  执行以下命令将文件拷贝到配置目录。

        ```
        cp cert_location /usr/local/etc/openvpn/
        ```

        `cert_location`是SSL客户端证书的下载路径，例如：/Users/example/Downloads/certs.zip。

    4.  执行以下命令将步骤四中下载的证书解压拷贝到配置目录。

        ```
        cd  /usr/local/etc/openvpn
        unzip /usr/local/etc/openvpn/certs.zip
        ```

    5.  执行以下命令发起连接，并完成用户名和密码验证。

        ```
        sudo /usr/local/opt/openvpn/sbin/openvpn --config /usr/local/etc/openvpn/config.ovpn
        ```

        ![Mac客户端双因子认证](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4129684951/p102655.jpg)


## 步骤四：测试连通性

配置完成后，您可以通过`ping`命令测试与云上VPC的连通性。以下内容以Windows客户端为例，为您展示如何测试与云上VPC的连通性。

1.  打开Windows客户端的cmd窗口。

2.  通过`ping`命令`ping`VPC下的ECS实例的IP地址，验证通信是否正常。

    **说明：** 请确保测试的ECS实例的安全组规则允许Windows客户端远程连接。更多信息，请参见[安全组应用案例ECS安全组配置操作指南](/cn.zh-CN/安全/安全组/安全组应用案例.md)。

    经测试，Windows客户端可以正常访问ECS实例。

    ![测试连通性](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6860784951/p88540.png)


