# VPN网关常见问题

本文为您介绍VPN网关的常见问题及解答。

-   [VPN网关是否支持经典网络？](#section_sdq_n3h_xdb)
-   [本地站点通过IPsec-VPN接入VPC的前提条件是什么？](#section_tdq_n3h_xdb)
-   [跨地域VPC是否可以通过VPN网关互通？](#section_udq_n3h_xdb)
-   [哪些本地网关设备可以与阿里云VPN网关建立连接？](#section_vdq_n3h_xdb)
-   [每个VPN网关可以建立多少个IPsec连接？](#section_xdq_n3h_xdb)
-   [是否可以通过VPN网关访问Internet？](#section_ydq_n3h_xdb)
-   [VPC间互通流量是否经过Internet？](#section_zdq_n3h_xdb)
-   [是否支持在一个IPsec连接中配置多个对端网段？](#section_a2q_n3h_xdb)
-   [是否可以降低VPN网关配置？](#section_b2q_n3h_xdb)
-   [SSL-VPN发布前购买的VPN网关实例是否可以使用SSL-VPN功能？](#section_c2q_n3h_xdb)
-   [如何充分利用VPN网关带宽？](#section_x0y_qv5_8ux)
-   [VPN网关中如何为网络ACL配置规则？](#section_3xk_61a_y9r)

## VPN网关是否支持经典网络？

不支持。VPN网关仅支持专有网络，如果您想在经典网络中使用VPN网关，需要在专有网络中开启ClassicLink功能。详细信息，请参见[在经典网络中使用IPsec-VPN](/cn.zh-CN/最佳实践/在经典网络中使用IPsec-VPN.md)。

## 本地站点通过IPsec-VPN接入VPC的前提条件是什么？

本地站点需要一个静态公网IP和一个支持IKEv1和IKEv2协议的网关设备，并且VPC和本地站点之间需要互通的两个网段不冲突。详细信息，请参见[t13351.md\#](/cn.zh-CN/IPsec-VPN入门/建立VPC到本地数据中心的连接.md)。

## 跨地域VPC是否可以通过VPN网关互通？

可以。详细信息，请参见[建立VPC到VPC的连接](/cn.zh-CN/用户指南/配置IPsec-VPN/建立VPC到VPC的连接.md)。

## 哪些本地网关设备可以与阿里云VPN网关建立连接？

阿里云VPN网关支持标准的IKEv1和IKEv2协议。因此，只要支持这两种协议的设备都可以和云上VPN网关互连，例如华为、华三、山石、深信服、Cisco ASA、Juniper、SonicWall、Nokia、IBM和Ixia等。详细信息，请参见[华三防火墙配置](/cn.zh-CN/用户指南/配置IPsec-VPN/本地网关配置/华三防火墙配置.md)。

## 每个VPN网关可以建立多少个IPsec连接？

每个VPN网关默认支持创建10个IPsec连接。如需创建更多IPsec连接，请提升配额。详细信息，请参见[管理配额](/cn.zh-CN/用户指南/管理配额.md)。

## 是否可以通过VPN网关访问Internet？

不可以。VPN网关仅提供私网接入VPC功能，不提供Internet访问的功能。

## VPC间互通流量是否经过Internet？

不经过。通过VPN网关实现跨地域VPC互连，流量只经过阿里云网络，不经过Internet。

## 是否支持在一个IPsec连接中配置多个对端网段？

支持。如果一个IPsec连接配置多个对端网段，建议IKE版本选择IKEv2。

## 是否可以降低VPN网关配置？

可以。如需降低VPN网关配置，请[提交工单](https://selfservice.console.aliyun.com/ticket/category/vpn/today)。

## SSL-VPN发布前购买的VPN网关实例是否可以使用SSL-VPN功能？

SSL-VPN发布前购买的VPN网关实例无法使用SSL-VPN功能。如需使用，请[提交工单](https://selfservice.console.aliyun.com/ticket/category/vpn/today)。

## 如何充分利用VPN网关带宽？

一条IPsec连接支持的最大带宽峰值为200M，如果您的VPN网关的带宽峰值大于200M，您可以通过创建多条IPsec连接实现充分利用VPN网关带宽。

例如，您的VPN网关的带宽峰值为800M，云上私网网段为10.0.0.0/8，云下私网网段为192.168.0.0/24，您可以配置4条IPsec连接，每条IPsec连接的本端网段和对端网段的配置如下：

-   IPsec连接1

    本端网段：10.0.0.0/10，对端网段：192.168.0.0/24

-   IPsec连接2

    本端网段：10.64.0.0/10，对端网段：192.168.0.0/24

-   IPsec连接3

    本端网段：10.128.0.0/10，对端网段：192.168.0.0/24

-   IPsec连接4

    本端网段：10.192.0.0/10，对端网段：192.168.0.0/24


其他参数配置，请参见[建立VPC到本地数据中心的连接](/cn.zh-CN/IPsec-VPN入门/建立VPC到本地数据中心的连接.md)。

## VPN网关中如何为网络ACL配置规则？

-   如果您在VPN所在的子网中使用了网络ACL，需要在网络ACL的出方向和入方向分别配置规则允许放行：100.104.0.0/16。
-   如果在SSL-VPN中使用了网络ACL，网络ACL需配置规则允许放行1194端口。

