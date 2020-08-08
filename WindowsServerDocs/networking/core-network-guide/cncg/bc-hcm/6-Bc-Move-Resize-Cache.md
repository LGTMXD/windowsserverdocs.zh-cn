---
title: 移动并调整托管缓存的大小（可选）
description: 本指南说明如何在运行 Windows Server 2016 和 Windows 10 的计算机上以托管缓存模式部署 BranchCache
manager: brianlic
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8eed5b91d0634a8409b6b6e26f823ffe86ea8a14
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964263"
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>移动托管缓存并调整其大小（ \( 可选）\)

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

可以使用此过程将托管缓存移到所需的驱动器和文件夹，并指定托管缓存服务器可用于托管缓存的磁盘空间量。

此过程是可选的。 如果默认缓存位置 \( % windir% \\ ServiceProfiles \\ NetworkService \\ AppData \\ 本地 \\ PeerDistPub \) 和 size （总硬盘空间的5%）适用于你的部署，则无需更改它们。

您必须是 Administrators 组的成员才能执行此过程。

### <a name="to-move-and-resize-the-hosted-cache"></a>移动托管缓存并调整其大小

1. 以管理员权限打开 Windows PowerShell。

2. 键入以下命令，将托管缓存移到本地计算机上的其他位置，然后按 ENTER。

    > [!IMPORTANT]
    > 运行以下命令之前，请将参数值（如– Path 和– MoveTo）替换为适用于你的部署的值。

    ```
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ```

3.  键入以下命令来调整托管缓存的大小，尤其是 \- 本地计算机上的 datacache。 按 Enter。

    > [!IMPORTANT]
    > 运行以下命令之前，请将参数值（如 \- 百分比）替换为适用于你的部署的值。

    ```
    Set-BCCache -Percentage 20
    ```

4.  若要验证托管缓存服务器配置，请键入以下命令，然后按 ENTER。

    ```
    Get-BCStatus
    ```

    命令的结果显示 BranchCache 安装的所有方面的状态。 下面是一些 BranchCache 设置，以及每个项的正确值：

    -   DataCache |CacheFileDirectoryPath：显示与通过 SetBCCache 命令的– MoveTo 参数一起提供的值匹配的硬盘位置。 例如，如果提供的值为 D： \\ datacache，则在命令输出中显示该值。

    -   DataCache |MaxCacheSizeAsPercentageOfDiskVolume：显示与通过 SetBCCache 命令的–百分率参数一起提供的值匹配的数字。 例如，如果提供的值为20，则该值将显示在命令输出中。

若要继续学习本指南，请参阅[Prehash 和预加载托管缓存服务器上的内容 &#40;可选&#41;](7-Bc-Prehash-Preload.md)。