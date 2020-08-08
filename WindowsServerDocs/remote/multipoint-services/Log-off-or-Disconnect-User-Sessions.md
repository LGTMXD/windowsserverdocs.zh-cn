---
title: 注销或断开用户会话
description: 了解如何手动注销用户
ms.topic: article
ms.assetid: 3e9bbcdc-e33b-481e-8b46-787a4f6d58bc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 0436f33df87da55792ba01a581c8f5c05f3500ce
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969324"
---
# <a name="log-off-or-disconnect-user-sessions"></a>注销或断开用户会话
MultiPoint 服务用户可以登录和注销其桌面会话，就像他们处理 Windows 会话一样。 用户还可以断开或挂起其会话，以便不使用 MultiPoint 服务工作站，但其会话在 MultiPoint 服务系统的计算机内存中保持活动状态。

此外，如果用户已从其 MultiPoint 服务会话中删除或忘记了注销系统，则管理用户可以结束用户会话。

## <a name="logging-off-or-disconnecting-a-session"></a>注销或断开会话
下表介绍了你或任何用户可以用以注销、挂起或结束会话的不同选项。

|||
|-|-|
|**操作**|**效果**|
|依次单击 "**开始**"、"设置"、 (右上角的 "用户名") ，然后单击 "**注销**"。|会话将结束且任何用户都可登录工作站。|
|依次单击“开始”****、“设置”****、“电源”，然后单击“断开”****。|将断开会话并将其保留在计算机内存中。 工作站可以由同一用户或其他用户登录。|
|依次单击 "**开始**"、"设置"、 (右上角的 "用户名") ，然后单击 "**锁定**"。|将锁定工作站并会将会话保留在计算机内存中。|

## <a name="suspending-or-ending-a-users-session"></a>挂起或结束用户会话
下表描述了你作为管理用户可用于断开或结束用户会话的不同选项。

|||
|-|-|
|**操作**|**效果**|
|**挂起：** 在 MultiPoint 管理器中，使用 "**工作站**" 选项卡来挂起用户会话。 有关详细信息，请参阅[挂起用户会话并使其保持为活动状态](Suspend-and-Leave-User-Session-Active.md)主题。|用户的会话将结束并保留在计算机内存中。 工作站可以由同一用户或其他用户登录。 用户可以登录到同一工作站或另一工作站，然后继续工作。|
|**结束：** 在 MultiPoint 管理器中，使用 "**工作站**" 选项卡来结束用户会话。 你还可以在 "**工作站**" 选项卡上结束所有用户会话。有关详细信息，请参阅[结束用户会话](End-a-User-Session.md)主题。|用户的会话将结束，并且任何用户都可以使用工作站。 用户的会话将不再显示在 "**工作站**" 选项卡上，也不会在计算机内存中显示。|

## <a name="see-also"></a>另请参阅
[暂停用户会话并使其保持活动状态](Suspend-and-Leave-User-Session-Active.md) 
[结束用户会话](End-a-User-Session.md) 
[管理用户桌面](manage-user-desktops-using-multipoint-dashboard.md) 
注销[用户会话](Log-Off-User-Sessions.md)