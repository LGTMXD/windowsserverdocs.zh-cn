---
title: 启用或禁用引用和客户端故障回复
description: 本文介绍如何启用或禁用引用和客户端故障回复。
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 0336588dcf0c170698c89b32a29952916bd26100
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954754"
---
# <a name="enable-or-disable-referrals-and-client-failback"></a>启用或禁用引用和客户端故障回复

> 适用于： Windows Server 2019，Windows Server (半年通道) ，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012，Windows Server 2008 R2，Windows Server 2008

引用是指当用户访问命名空间根目录或包含目标的 DFS 文件夹时，客户端计算机从域控制器或命名空间服务器接收的服务器的排序列表。 接收引用后，计算机会尝试访问列表中的第一个服务器。 如果该服务器不可用，则客户端计算机会尝试访问下一个服务器。 如果服务器不可用，则可将客户端配置为在该服务器可用后故障回复到首选服务器。

以下部分提供有关如何启用或禁用引用或启用客户端故障回复的信息：

## <a name="enable-or-disable-referrals"></a>启用或禁用引用

通过禁用命名空间服务器的引用或文件夹目标的引用，可以防止用户被定向到该命名空间服务器或文件夹目标。 如果需要临时使服务器脱机以便进行维护，此功能很有用。

-   若要启用或禁用对文件夹目标的引用，请按照以下步骤操作：

    1.  在 DFS 管理控制台树中的**命名空间**节点下，单击包含目标的文件夹，然后在**详细信息**窗格中单击**文件夹目标**。
    2.  右键单击该文件夹目标，然后单击**禁用文件夹目标**或**启用文件夹目标**。

-   若要启用或禁用对命名空间服务器的引用，请按照以下步骤操作：

    1.  在 DFS 管理控制台树中，选择相应的命名空间，然后单击**命名空间服务器**选项卡。
    2.  右键单击相应的命名空间服务器，然后单击**禁用命名空间服务器**或**启用命名空间服务器**。


> [!TIP]
> 若要使用 Windows PowerShell 启用或禁用引用，请使用 [Set-DfsnRootTarget –State](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731089(v=ws.11)) 或 [Set-DfsnServerConfiguration](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731089(v=ws.11)) cmdlet（在 Windows Server 2012 中引入）。

## <a name="enable-client-failback"></a>启用客户端故障回复

如果目标不可用，可以将客户端配置为在目标恢复后故障回复到该目标。 若要使故障回复正常进行，客户端计算机必须满足以下主题中所列的要求：[查看 DFS 命名空间客户端要求](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11))。


> [!NOTE]
> 若要使用 Windows PowerShell 对命名空间根目录启用客户端故障回复，请使用 [Set-DfsnRoot](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11)) cmdlet。 若要对 DFS 文件夹启用客户端故障回复，请使用 [Set-DfsnFolder](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11)) cmdlet。


## <a name="to-enable-client-failback-for-a-namespace-root"></a>对命名空间根路径启用客户端故障回复的步骤

1.  单击“开始”****、指向“管理工具”****，然后单击“DFS 管理”****。

2.  在控制台树中的“命名空间”**** 节点下，右键单击命名空间，然后单击“属性”****。

3.  在“引用”**** 选项卡上，选中“客户端故障回复到首选目标”**** 复选框。

包含目标的文件夹从命名空间根路径继承客户端故障回复设置。 如果对命名空间根目录禁用了客户端故障回复，则可按照以下过程使客户端可对包含目标的文件夹启用故障回复。

## <a name="to-enable-client-failback-for-a-folder-with-targets"></a>对包含目标的文件夹启用客户端故障回复的步骤

1.  单击“开始”****、指向“管理工具”****，然后单击“DFS 管理”****。

2.  在控制台树中的“命名空间”**** 节点下，右键单击包含目标的文件夹，然后单击“属性”****。

3.  在“引用”**** 选项卡上，单击“客户端故障回复到首选目标”**** 复选框。

## <a name="additional-references"></a>其他参考

-   [调整 DFS 命名空间](tuning-dfs-namespaces.md)
-   [查看 DFS 命名空间客户端要求](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771913(v=ws.11))
-   [委派 DFS 命名空间的管理权限](delegate-management-permissions-for-dfs-namespaces.md)
