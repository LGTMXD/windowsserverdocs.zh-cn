---
title: 文件服务器资源管理器疑难解答
description: 本文介绍如何解决在使用文件服务器资源管理器时遇到的常见问题
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: fbd44938f57cc27576ba3d3bfa39b3e87e4989ed
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950441"
---
# <a name="troubleshooting-file-server-resource-manager"></a>文件服务器资源管理器疑难解答

> 适用于： Windows Server 2019，Windows Server 2016，Windows Server (半年通道) ，Windows Server 2012 R2，Windows Server 2012，Windows Server 2008 R2

本部分列出了在使用文件服务器资源管理器时可能遇到的常见问题。

> [!Note]
> 一个不错的疑难解答选项就是查看文件服务器资源管理器生成的事件日志。 文件服务器资源管理器的所有事件日志项均位于源 **SRMSVC** 下的**应用程序**事件日志中

## <a name="i-am-not-receiving-e-mail-notifications"></a>我无法接收电子邮件通知。

-   **原因**：电子邮件选项尚未配置，或配置不正确。

-   **解决方案**：在**电子邮件通知**选项卡上，在**文件服务器资源管理器选项**对话框中验证 SMTP 服务器和默认的电子邮件收件人是否已指定和有效。 发送测试电子邮件以确认信息正确，且用于发送通知的 SMTP 服务器正常工作。 有关详细信息，请参阅[配置电子邮件通知](configure-email-notifications.md)。


## <a name="i-am-only-receiving-one-e-mail-notification-even-though-the-event-that-triggered-that-notification-happened-several-times-in-a-row"></a>我只接收到一个电子邮件通知，即使触发该通知的事件连续多次发生也是如此。

-   **原因**：如果用户多次尝试保存已被阻止的文件或保存超出配额阈值的文件，并且存在针对该文件屏蔽或配额事件配置的电子邮件通知，则默认情况下在 60 分钟内只会向管理员发送一封电子邮件。 这可防止管理员的电子邮件帐户中出现大量重复的消息。

-   **解决方案**：在**通知限制**选项卡上，可以在**文件服务器资源管理器选项**对话框中为每种通知类型设置时间限制：电子邮件、事件日志、命令和报告。 对于相同的问题，每项限制都会指定一个生成另一相同类型的通知前必须经过的时间段。 有关详细信息，请参阅[配置通知限制](configure-notification-limits.md)。


## <a name="my-storage-reports-keep-failing-and-little-or-no-information-is-available-in-the-event-log-regarding-the-source-of-the-failure"></a>我的存储报告总是出现故障，并且事件日志中几乎没有或完全没有关于故障原因的可用信息。

-   **原因**：保存报告的卷可能损坏。
-   **解决方案**：在卷中运行 **chkdsk** 并尝试再次生成报告。

## <a name="my-file-screening-audit-reports-do-not-contain-any-information"></a>我的文件屏蔽审核报告中没有任何信息。

-   **原因**：可能由于以下一个或多个原因：
    -   审核数据库未配置为记录文件屏蔽活动。
    -   审核数据库为空（即未记录任何文件屏蔽活动）。
    -   文件屏蔽审核报告的参数未从审核数据库中选择数据。

-   **解决方案**：在**文件屏蔽审核**选项卡上，在**文件服务器资源管理器选项**对话框中验证**在审核数据库中记录文件屏蔽活动**复选框是否已选中。
    -   有关记录文件屏蔽活动的详细信息，请参阅[配置文件屏蔽审核](configure-file-screen-audit.md)。
    -   若要配置文件屏蔽审核报告的默认参数，请参阅[配置存储报告](configure-storage-reports.md)。
    -   若要编辑计划报告任务或按需报告的报告参数，请参阅[存储报告管理](storage-reports-management.md)。

## <a name="the-used-and-available-values-for-some-of-the-quotas-i-have-created-do-not-correspond-to-the-actual-limit-setting"></a>我创建的部分配额的“已使用”和“可用”值与实际的“限制”设置不对应。

-   **原因**：可能存在嵌套配额，其中子文件夹的配额从其父文件夹的配额派生出一个更严格的限制。 例如，可能将一个 100 兆字节 (MB) 的配额限制应用于父文件夹，并将一个 200 MB 的配额分别应用于其中的每一个子文件夹。 如果父文件夹中共存储了 50 MB 的数据（存储在其子文件夹中的数据总量），则每一个子文件夹将仅列出 50 MB 的可用空间。

-   **解决方案**：在**配额管理**下，单击**配额**。 在**结果**窗格中，选择正在解决的配额项。 在**操作**窗格中，单击**查看影响文件夹的配额**，然后查找应用于父文件夹的配额。 这将能够确定哪些父文件夹配额拥有低于所选配额的存储限制设置。

