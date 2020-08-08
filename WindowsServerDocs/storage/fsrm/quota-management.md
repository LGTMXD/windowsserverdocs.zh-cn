---
title: 定额管理
description: 本文介绍了如何创建和管理配额
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b1d2d37d73a3d7837fd5390b9f5860f7cb41ee85
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961371"
---
# <a name="quota-management"></a>定额管理

> 适用于： Windows Server 2019，Windows Server 2016，Windows Server (半年通道) ，Windows Server 2012 R2，Windows Server 2012，Windows Server 2008 R2

可在文件服务器资源管理器 Microsoft<sup>®</sup> 管理控制台 (MMC) 管理单元的**配额管理**节点上执行以下任务：

-   创建配额以限制卷或文件夹拥有的空间，并在接近或超过配额限制时生成通知。
-   生成自动应用配额，以便应用于卷或文件夹中所有现有子文件夹，及将来创建的任何子文件夹。
-   定义可轻松应用于新卷或文件夹以及可在组织中使用的配额模板。

例如，你可以：

-   为用户的个人服务器文件夹设置 200 兆字节 (MB) 的限额，当存储内容超过 180 MB 时，你和用户将收到电子邮件通知。
-   对组的共享文件夹设置灵活的 500 MB 配额。 达到此存储限制时，将通过电子邮件通知组中的所有用户，存储配额已临时扩展到 520 MB，以便用户可以删除不必要的文件并符合预设的 500 MB 配额策略。
-   当所使用的临时文件夹达到 2 千兆字节 (GB) 时，系统会发出通知，但不会限制该文件夹的配额，因为在服务器上运行服务需要一定空间。

本节包括下列主题：

-   [创建配额](create-quota.md)
-   [创建自动应用配额](create-auto-apply-quota.md)
-   [创建配额模板](create-quota-template.md)
-   [编辑配额模板属性](edit-quota-template-properties.md)
-   [编辑自动应用配额属性](edit-auto-apply-quota-properties.md)

> [!Note]
> 若要设置电子邮件通知和报告功能，首先必须配置文件服务器资源管理器常规选项。

## <a name="additional-references"></a>其他参考

-   [设置文件服务器资源管理器选项](setting-file-server-resource-manager-options.md)


