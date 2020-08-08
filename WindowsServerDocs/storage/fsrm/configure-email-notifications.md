---
title: 配置电子邮件通知
description: 本文介绍如何配置电子邮件通知
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 71a9f75d84aafcd852ae71494d133dda91e848f1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954684"
---
# <a name="configure-e-mail-notifications"></a>配置电子邮件通知

> 适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

在创建配额和文件屏蔽时，可以选择在接近配额限制时或者在用户尝试保存已阻止的文件后向用户发送电子邮件通知。 生成存储报告时，可以选择通过电子邮件将报告发送给特定收件人。 如果希望向特定管理员例行通知配额和文件屏蔽事件，或者发送存储报告，则可以配置一个或多个默认的收件人。

若要发送这些通知和存储报告，必须指定用于转发电子邮件的 SMTP 服务器。

## <a name="to-configure-e-mail-options"></a>若要配置电子邮件选项，请执行以下操作：

1. 在控制台树中，右键单击**文件服务器资源管理器**，然后单击**配置选项**。 此时将打开“文件服务器资源管理器选项”**** 对话框。

2. 在**电子邮件通知**选项卡上的** SMTP 服务器名称或 IP 地址**下，键入将转发电子邮件通知和存储报告的 SMTP 服务器的主机名或 IP 地址。

3. 如果希望向特定管理员例行通知配额或文件屏蔽事件，或通过电子邮件发送存储报告，请在**默认的管理员收件人**下键入每个电子邮件地址。

   使用格式 <em>account@domain</em> 。 使用分号分隔多个帐户。

4. 若要为文件服务器资源管理器发出的电子邮件通知和存储报告指定不同的“发件人”地址，请在**默认“发件人”电子邮件地址**下键入希望在电子邮件中显示的电子邮件地址。

5. 若要测试你的设置，请单击**发送测试电子邮件**。

6. 单击“确定”。


## <a name="additional-references"></a>其他参考

-   [设置文件服务器资源管理器选项](setting-file-server-resource-manager-options.md)