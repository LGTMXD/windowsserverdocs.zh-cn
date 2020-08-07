---
title: 管理多个 Active Directory 林中的资源
description: 本主题是 Windows Server 2016 中的 IP 地址管理 (IPAM) 管理指南的一部分。
manager: brianlic
ms.topic: article
ms.assetid: 82f8f382-246e-4164-8306-437f7a019e0f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ccfe766651600da146843c8db947df0f61c667dc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964063"
---
# <a name="manage-resources-in-multiple-active-directory-forests"></a>管理多个 Active Directory 林中的资源

>适用于：Windows Server（半年频道）、Windows Server 2016

你可以使用本主题来了解如何使用 IPAM 管理多个 Active Directory 林中的域控制器、DHCP 服务器和 DNS 服务器。

要使用 IPAM 管理远程 Active Directory 林中的资源，要管理的每个林都必须与安装 IPAM 的林有双向信任关系。

若要为不同的 Active Directory 林启动发现过程，请打开服务器管理器并单击 "IPAM"。 在 IPAM 客户端控制台中，单击 "**配置服务器发现**"，然后单击 "**获取林**"。 这会启动一个可发现受信任林及其域的后台任务。 发现过程完成后，请单击 "**配置服务器发现**"，这将打开下列对话框。

![配置服务器发现](../../media/Manage-Resources-in-Multiple-Active-Directory-Forests/ipam_serverdiscovery.jpg)

>[!NOTE]
>对于 \- Active Directory 跨林方案进行基于组策略的预配，请确保在 IPAM 服务器上运行以下 Windows PowerShell cmdlet，而不是在信任域 dc 上运行。 例如，如果你的 IPAM 服务器已加入到林 corp.contoso.com 并且信任林为 fabrikam.com，则可以在 corp.contoso.com for azure 中的 IPAM 服务器上运行以下 Windows PowerShell cmdlet，以在 \- fabrikam.com 林上进行基于组策略的预配。 若要运行此 cmdlet，你必须是 fabrikam.com 林中的 Domain Admins 组的成员。

```powershell
    Invoke-IpamGpoProvisioning -Domain fabrikam.COM -GpoPrefixName IPAMSERVER -IpamServerFqdn IPAM.CORP.CONTOSO.COM
```

在 "**配置服务器发现**" 对话框中，单击 "**选择林**"，然后选择要用 IPAM 管理的林。 同时选择要管理的域，然后单击 "**添加**"。

在 "**选择要发现的服务器角色**" 中，为要管理的每个域指定要发现的服务器类型。 选项为**域控制器**、 **DHCP 服务器**和**DNS 服务器**。

默认情况下，会发现域控制器、DHCP 服务器和 DNS 服务器，因此，如果您不想发现其中一种类型的服务器，请确保取消选中该选项的复选框。

在上面的示例图中，IPAM 服务器安装在 contoso.com 林中，并为 IPAM 管理添加了 fabrikam.com 林的根域。 所选服务器角色允许 IPAM 发现和管理 fabrikam.com 根域和 contoso.com 根域中的域控制器、DHCP 服务器和 DNS 服务器。

指定林、域和服务器角色后，单击 **"确定"**。 IPAM 执行发现，在发现完成后，你可以管理本地和远程林中的资源。
