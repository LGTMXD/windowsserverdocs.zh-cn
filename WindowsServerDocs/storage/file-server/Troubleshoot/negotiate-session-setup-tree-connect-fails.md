---
title: 协商、会话设置和树连接故障
description: 介绍如何对协商、会话设置和树连接失败进行故障排除。
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 2bad602f934d844074ee96df06bf9234fdbf943f
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961159"
---
# <a name="negotiate-session-setup-and-tree-connect-failures"></a>协商、会话设置和树连接故障

本文介绍如何解决在 SMB 协商、会话设置和树连接请求过程中出现的故障。

## <a name="negotiate-fails"></a>协商失败

SMB 服务器从 SMB 客户端接收 SMB 协商请求。 连接超时，在60秒后重置。 大约200微秒后可能会出现 ACK 消息。

此问题最常见的原因是防病毒程序。

如果使用的是 Windows Server 2008 R2，则存在此问题的修补程序。 请确保 SMB 客户端和 SMB 服务器都是最新的。

## <a name="session-setup-fails"></a>会话安装失败

SMB 服务器 \_ 从 smb 客户端接收 SMB 会话安装请求，但未能响应。

如果服务器的完全限定的域名（FQDN）或网络基本输入/输出系统（NetBIOS）名称为 "sed" （通用命名约定（UNC）路径），则 Windows 将使用 Kerberos 进行身份验证。

协商响应后，将尝试获取服务器的通用 Internet 文件系统（CIFS）服务主体名称（SPN）的 Kerberos 票证。 查看 TCP 端口88上的 Kerberos 流量，确保 SMB 客户端正在获取令牌时不会出现 Kerberos 错误。

> [!NOTE]
> 在 Kerberos 预身份验证期间发生的错误都是正常的。 在 Kerberos 预身份验证（身份验证不起作用的实例）之后发生的错误是导致 SMB 问题的错误。

此外，请进行以下检查：

- 查看 SMB 会话安装请求中的安全 blob \_ ，以确保发送正确的凭据。

- 尝试禁用 SMB 服务器名称强化（**SmbServerNameHardeningLevel = 0**）。

- 请确保 SMB 服务器在通过 CNAME DNS 记录访问时具有 SPN。

- 请确保 SMB 签名正常运行。 （这对于较早的第三方设备尤其重要。）

## <a name="tree-connect-fails"></a>树连接失败

请确保用户帐户凭据具有对文件夹的共享和 NT 文件系统（NTFS）权限。

常见树连接错误的原因可以在[接收 SMB2 树 \_ 连接请求的 3.3.5.7](/openspecs/windows_protocols/ms-smb2/652e0c14-5014-4470-999d-b174d7b2da87)中找到。 下面是两个常见状态代码的解决方案。

\[状态 \_ 错误的 \_ 网络 \_ 名称\]

请确保该共享存在于服务器上，并且在 SMB 客户端请求中拼写正确。

\[\_拒绝访问 \_ 状态\]

验证共享所使用的磁盘和文件夹是否存在并且是否可访问。

如果使用 SMBv3 或更高版本，请检查服务器和共享是否需要加密，但客户端不支持加密。 为此，请执行以下操作：

- 通过运行以下命令来检查服务器。

  ```PowerShell
  Get-SmbServerConfiguration | select Encrypt*
  ```

  如果 EncryptData 和 RejectUnencryptedAccess 为 true，则服务器要求加密。

- 通过运行以下命令来检查共享：

  ```PowerShell
  Get-SmbShare | select name, EncryptData  
  ```

  如果在共享上 EncryptData 为 true，并且服务器上的 RejectUnencryptedAccess 为 true，则表示共享需要加密

在进行故障排除时，请遵循以下准则：

- Windows 8、Windows Server 2012 和更高版本的 Windows 支持客户端加密（SMBv3 和更高版本）。

- Windows 7、Windows Server 2008 R2 和更早版本的 Windows 不支持客户端加密。

- Samba 和第三方设备可能不支持加密。 可能需要参考产品文档来了解详细信息。

## <a name="references"></a>参考资料

有关详细信息，请参阅以下文章。

[3.3.5.4 接收 SMB2 协商请求](/openspecs/windows_protocols/ms-smb2/b39f253e-4963-40df-8dff-2f9040ebbeb1)

[3.3.5.5 接收 SMB2 会话 \_ 安装请求](/openspecs/windows_protocols/ms-smb2/e545352b-9f2b-4c5e-9350-db46e4f6755e)

[3.3.5.7 接收 SMB2 树 \_ 连接请求](/openspecs/windows_protocols/ms-smb2/652e0c14-5014-4470-999d-b174d7b2da87)
