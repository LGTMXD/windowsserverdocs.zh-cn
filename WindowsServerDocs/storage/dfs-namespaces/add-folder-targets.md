---
title: 添加文件夹目标
description: 本主题介绍如何添加文件夹目标（UNC 路径）
ms.prod: windows-server
ms.author: jgerend
manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms-date: 06/05/2017
ms.openlocfilehash: 2f4e0deb82f16c905f580c13115a5214556d4f5f
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475554"
---
# <a name="add-folder-targets"></a>添加文件夹目标

> 适用于： Windows Server 2019，Windows Server （半年频道），Windows Server 2016，Windows Server 2012 R2，Windows Server 2012，Windows Server 2008 R2，Windows Server 2008

文件夹目标是共享文件夹或与命名空间中的某个文件夹关联的另一个命名空间的通用命名约定 (UNC) 路径。 添加多个文件夹目标可增加命名空间中的文件夹的可用性。

## <a name="to-add-a-folder-target"></a>添加文件夹目标

若要使用 DFS 管理添加文件夹目标，请按照以下过程操作：

1.  单击“开始”****、指向“管理工具”****，然后单击“DFS 管理”****。

2.  在控制台树中的**命名空间**节点下，右键单击某文件夹，然后单击**添加文件夹目标**。

3.  键入该文件夹目标的路径，或者单击**浏览**以找到该文件夹目标。

4.  如果使用 DFS 复制对文件夹进行复制，则可指定是否向复制组添加新文件夹目标。

> [!TIP]
> 若要使用 Windows PowerShell 添加文件夹目标，请使用 [New-DfsnFolderTarget](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnfoldertarget) cmdlet。 Windows Server 2012 中引入了 DFSN Windows PowerShell 模块。

> [!NOTE]
> 在文件夹层次结构中的相同级别，文件夹可以包含文件夹目标或其他 DFS 文件夹，但是不能同时包含二者。

## <a name="additional-references"></a>其他参考

-   [部署 DFS 命名空间](deploying-dfs-namespaces.md)
-   [委派 DFS 命名空间的管理权限](delegate-management-permissions-for-dfs-namespaces.md)
-   [使用 DFS 复制复制文件夹目标](replicate-folder-targets-using-dfs-replication.md)