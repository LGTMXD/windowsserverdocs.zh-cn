---
title: 配置文件屏蔽审核
description: 本文介绍如何配置文件屏蔽审核以生成文件屏蔽审核报告
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 822c483fc7f5f4518ca976b1f7d719b95730008f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950682"
---
# <a name="configure-file-screen-audit"></a>配置文件屏蔽审核

> 适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

通过使用文件服务器资源管理器，可以在审核数据库中记录文件屏蔽活动。 此数据库中保存的信息可用于生成文件屏蔽审核报告。

> [!Important]
> 如果清除**在审核数据库中记录文件屏蔽活动**复选框，则文件屏蔽审核报告将不包含任何信息。

## <a name="to-configure-file-screen-audit"></a>若要配置文件屏蔽审核，请执行以下操作：

1.  在控制台树中，右键单击**文件服务器资源管理器**，然后单击**配置选项**。 此时将打开“文件服务器资源管理器选项”**** 对话框。

2.  选择**文件屏蔽审核**选项卡上的**在审核数据库中记录文件屏蔽活动**复选框。

3.  单击“确定”。 现在，所有文件屏蔽活动都将存储在审核数据库中，并可通过运行文件屏蔽审核报告进行查看。

## <a name="additional-references"></a>其他参考

-   [设置文件服务器资源管理器选项](setting-file-server-resource-manager-options.md)
-   [存储报告管理](storage-reports-management.md)