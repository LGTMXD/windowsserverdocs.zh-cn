---
title: 配置通知限制
description: 本文介绍如何为不同类型的通知添加时间限制
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 969c950d3a925afac400d128ac21ed0923f07ffa
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950651"
---
# <a name="configure-notification-limits"></a>配置通知限制

> 适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

若要减少为反复超过某个配额阈值或尝试保存未经授权的文件而累积的通知数量，文件服务器资源管理器会将时间限制应用于以下通知类型：

-   电子邮件
-   事件日志
-   Command
-   报表

对于相同的问题，每项限制都会指定一个生成另一相同类型的配置通知前的时间段。

每个通知类型的默认限制设置为 60 分钟，但你可以更改这些限制。 此项限制将应用于所有指定类型的通知，无论通知是由配额阈值还是文件屏蔽事件生成。

## <a name="to-specify-a-standard-notification-limit-for-each-notification-type"></a>若要为每个通知类型指定标准通知限制，请执行以下操作：

1.  在控制台树中，右键单击**文件服务器资源管理器**，然后单击**配置选项**。 此时将打开“文件服务器资源管理器选项”**** 对话框。

2.  在**通知限制**选项卡上，输入每个所显示的通知类型相应的值（分钟）。

3.  单击“确定”。

> [!Note]
> 若要自定义与特定配额或文件屏蔽通知相关的时间限制，可以使用文件服务器资源管理器命令行工具 **Dirquota.exe** 和 **Filescrn.exe**，或者使用[文件服务器资源管理器](/powershell/module/fileserverresourcemanager/?view=win10-ps) cmdlet。

## <a name="additional-references"></a>其他参考

-   [设置文件服务器资源管理器选项](setting-file-server-resource-manager-options.md)
-   [命令行工具](command-line-tools.md)
