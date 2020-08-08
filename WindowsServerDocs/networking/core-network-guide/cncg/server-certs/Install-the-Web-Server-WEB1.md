---
title: 安装 Web 服务器 WEB1
description: 本主题是指导 802.1 X 有线和无线部署的 "部署服务器证书" 的一部分
manager: brianlic
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 97ee8c257d9c84b63ee069d87d7bfa6ebf3299e4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949461"
---
# <a name="install-the-web-server-web1"></a>安装 Web 服务器 WEB1

>适用于：Windows Server（半年频道）、Windows Server 2016

Windows Server 2016 中的 Web 服务器 (IIS) 角色提供一个安全、易于管理的模块化和可扩展的平台，以可靠地托管网站、服务和应用程序。 使用 IIS，你可以与 Internet、intranet 或 extranet 上的用户共享信息。 IIS 是一个统一的 web 平台，它将 IIS、ASP.NET、FTP 服务、PHP 和 Windows Communication Foundation (WCF) 相集成。

部署服务器证书时，你的 Web 服务器将向你提供一个位置，你可以在其中为证书颁发机构 (CA)  (CRL) 发布证书吊销列表。 发布后，网络上的所有计算机都可以访问 CRL，以便他们可以在身份验证过程中使用此列表来验证其他计算机提供的证书是否未被吊销。

如果证书在 CRL 上被吊销，则身份验证工作将失败，并且你的计算机会受到保护，使其无法信任其证书不再有效的实体。

在安装 Web 服务器 (IIS) 角色之前，请确保已配置服务器名称和 IP 地址，并已将计算机加入域。

## <a name="to-install-the-web-server-iis-server-role"></a> (IIS) 服务器角色安装 Web 服务器
若要完成此过程，你必须是**Administrators**组的成员。

>[!NOTE]
>若要使用 Windows PowerShell 执行此过程，请打开 PowerShell，键入以下命令，然后按 ENTER。
`Install-WindowsFeature Web-Server -IncludeManagementTools`

1.  在“服务器管理器”中，单击“管理”****，然后单击“添加角色和功能”****。 将打开“添加角色和功能向导”。
2.  在“开始之前”**** 中单击“下一步”****。

**注意**如果你之前运行了 "添加角色和功能向导" 并且选择了 "**默认情况下跳过此页**"，则不会显示 "添加角色和功能向导" 的 "**开始之前**" 页。

3. 在 **“安装类型”** 页上，单击 **“下一步”**。
4. 在 "**服务器选择**" 页上，单击 "**下一步**"。
5. 在 "**服务器角色**" 页上，选择 " **WEB 服务器 (IIS) **，然后单击"**下一步**"。
6. 单击 **“下一步”** 直到接受了所有默认的 web 服务器设置，然后单击 **“安装”**。
7. 验证是否所有安装都已成功，然后单击“关闭”****。
