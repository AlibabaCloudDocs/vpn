# Overview

This topic describes how to remotely access a virtual private cloud \(VPC\) through SSL-VPN.

## Prerequisites

Before you start, make sure the following requirements are met:

-   The private CIDR block of the VPC cannot overlap with that of the client. Otherwise, the client cannot communicate with the VPC.
-   The client can access the Internet.

## Procedure

The following figure describes the procedure for configuring remote access to a VPC through SSL-VPN.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0322029951/p41027.png)

1.  Create a VPN gateway

    Create a VPN gateway and enable the SSL-VPN feature.

2.  Create an SSL server

    Specify the CIDR blocks of the SSL server and client to be connected.

3.  Create a client certificate

    Create a client certificate based on the SSL server configuration, and then download the client certificate and the configuration file.

4.  Configure the client

    Download and install the VPN client, and then load the client certificate and the configuration file to the client.

5.  Configure a security group

    Make sure that the rules in the security group of the Elastic Compute Service \(ECS\) instances allow remote access from the client.


