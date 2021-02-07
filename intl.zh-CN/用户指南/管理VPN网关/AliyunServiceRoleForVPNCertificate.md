# AliyunServiceRoleForVPNCertificate

本文为您介绍VPN网关的服务关联角色AliyunServiceRoleForVPNCertificate以及如何删除VPN网关服务关联角色。

## 背景信息

服务关联角色SLR（Service Linked Role）是指与某个云服务关联的RAM角色。在某些场景下，为了完成云服务的某个功能，需要获取其他云服务的访问权限。通过服务关联角色，您可以更好的创建云服务正常操作所需的权限，避免误操作带来的风险。关于服务关联角色的更多信息，请参见[服务关联角色](/intl.zh-CN/角色管理/服务关联角色.md)。

## 创建服务关联角色AliyunServiceRoleForVPNCertificate

您在首次绑定国密型VPN网关和国密证书时，系统将会为您自动创建一个名称为AliyunServiceRoleForVPNCertificate的服务关联角色，并且为该角色添加名称为AliyunServiceRolePolicyForVPNCertificate的权限策略，该权限会允许VPN网关访问其他云资源。权限策略内容如下：

**说明：** 如果服务关联角色AliyunServiceRoleForVPNCertificate已存在，系统则不会重复创建。

```
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "kms:DescribeCertificate",
        "kms:GetCertificate",
        "kms:CertificatePublicKeyEncrypt",
        "kms:CertificatePrivateKeyDecrypt",
        "kms:CertificatePublicKeyVerify",
        "kms:CertificatePrivateKeySign"
      ],
      "Resource": "*"
    },
    {
      "Action": "ram:DeleteServiceLinkedRole",
      "Resource": "*",
      "Effect": "Allow",
      "Condition": {
        "StringEquals": {
          "ram:ServiceName": "certificate.vpn.aliyuncs.com"
        }
      }
    }
  ],
  "Version": "1"
}
```

## 删除服务关联角色AliyunServiceRoleForVPNCertificate

系统不会自动删除VPN网关的服务关联角色AliyunServiceRoleForVPNCertificate。如果您要删除VPN网关的服务关联角色AliyunServiceRoleForVPNCertificate，请确保当前阿里云账号下的国密型VPN网关与国密证书没有绑定关系。具体操作，请参见：

-   [解除国密证书]()
-   [删除服务关联角色](/intl.zh-CN/角色管理/服务关联角色.md)

## 相关文档

[绑定国密证书]()

