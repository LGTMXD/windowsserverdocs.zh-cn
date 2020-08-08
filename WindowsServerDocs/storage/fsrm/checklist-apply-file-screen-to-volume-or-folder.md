---
title: 清单 - 将文件屏蔽应用于卷或文件夹
description: 本文介绍如何将文件屏蔽应用于卷或文件夹
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e7318d2e67cb5dd39aaa4fb95ad6cbca7eff9512
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957595"
---
# <a name="checklist---apply-a-file-screen-to-a-volume-or-folder"></a>清单 - 将文件屏蔽应用于卷或文件夹

> 适用于： Windows Server 2019，Windows Server 2016，Windows Server (半年通道) ，Windows Server 2012 R2，Windows Server 2012，Windows Server 2008 R2

如要将文件屏蔽应用于卷或文件夹，请使用以下列表：
1. 若要按照[配置电子邮件通知](configure-email-notifications.md) 中的说明，通过电子邮件发送文件屏蔽通知或存储报告，则需配置电子邮件设置。

2. 若要生成文件屏蔽审核报告，请启用审核数据库中的文件屏蔽事件记录功能。
[配置文件屏蔽审核](configure-file-screen-audit.md)

3. 评估作为屏蔽规则候选项的已存储文件类型。 你可以使用**存储报告管理**节点的报告来提供数据。 （例如，根据需要运行“按文件组分类的文件”报告或“大文件”报告来确定占用大量磁盘空间的文件。）[根据需要生成报告](generate-reports-on-demand.md)

4. 查看预配置的文件组，或创建新文件组，从而在你的组织中强制执行特定屏蔽策略。 [定义用于屏蔽的文件组](define-file-groups-for-screening.md)

5. 查看可用文件屏蔽模板的属性。 (单击**文件屏蔽管理**中的**文件屏蔽模板**节点。)[编辑文件屏蔽模板属性](edit-file-screen-template-properties.md)
<br />
 -或-
 <br /> 创建新的文件屏蔽模板，在你的组织中强制执行存储策略。  [创建文件屏蔽模板](create-file-screen-template.md)

6. 基于卷或文件夹创建文件屏蔽。
 [创建文件屏蔽](create-file-screen.md)

7. 配置卷或文件夹的子文件夹中的文件屏蔽例外。 [创建文件屏蔽例外](create-file-screen-exception.md)

8. 计划一项包含文件屏蔽审计报告的报告任务，以定期监测屏蔽活动。
  [计划一组报告](schedule-set-of-reports.md)


> [!NOTE]
> 若要限制卷或文件夹的存储空间，请参阅[清单：将配额应用于卷或文件夹](checklist-apply-file-screen-to-volume-or-folder.md)