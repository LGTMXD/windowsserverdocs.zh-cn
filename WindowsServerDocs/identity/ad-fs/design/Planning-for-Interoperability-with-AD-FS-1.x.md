---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: 规划与 AD FS 1.x 的互操作性
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 94313fc185a4f326ad00a95e4c594fd3e696f61a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967604"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>规划与 AD FS 1.x 的互操作性

Active Directory 联合身份验证服务 \( AD FS \) 运行 windows server 2012 的联合服务器 &reg; 可以与随 \( windows server 2003 R2 联合身份验证服务一起安装的 AD FS 1.0 \) 和 \( 使用 windows Server 2008 或 windows server 2008 r2 AD FS 安装的联合身份验证服务1.1 互操作 \) 。 支持以下任何互操作性组合：

-   任何 AD FS 1。*x*联合身份验证服务可以发送可由 Windows Server 2012 中的 AD FS 联合身份验证服务使用的声明。 有关详细信息，请参阅[清单：将 AD FS 配置为使用 AD FS 1.x 中的声明](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)。

-   Windows Server 2012 中的任何 AD FS 联合身份验证服务都可以发送 AD FS 1。*x* \-可由 AD FS 1 使用的兼容声明。*x*联合身份验证服务。 有关详细信息，请参阅 [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)。

-   Windows Server 2012 中的任何 AD FS 联合身份验证服务都可以发送 AD FS 1。*x* \-运行 AD FS 1 的一台或多台 Web 服务器可以使用的兼容声明。*x*声明 \- 感知 Web 代理。 有关详细信息，请参阅 [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)。

> [!NOTE]
> AD FS 不支持 AD FS 1 或与之进行互操作。基于*x* Windows NT 令牌的 Web 代理。

AD FS 1。*x* \-兼容声明是可以由 Windows Server 2012 中的 AD FS 联合身份验证服务发送并由 AD FS 1 理解的声明。*x*联合身份验证服务。 AD FS 1。*x*联合身份验证服务可以使用 AD FS 联合身份验证服务发送的声明， \( 必须发送名称标识符 ID \) 声明类型。

## <a name="understanding-the-name-id-claim-type"></a>了解名称 ID 声明类型
名称 ID 声明类型等效于 AD FS 1.*x* 使用的标识声明类型。 每当要与 AD FS 1.*x* 进行互操作时，都必须使用该类型。 名称 ID 声明类型启用 AD FS 1。*x*联合身份验证服务或 AD FS 1。*x*声明 \- 感知 Web 代理使用 Windows Server 2012 中 AD FS 的声明，前提是这些声明是使用下表中的名称 ID 格式之一发送的。


|      名称 ID 格式       |               对应 URI                |
|---------------------------|------------------------------------------------|
| AD FS 1。*x*电子邮件地址 | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* 电子邮件 UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        公用名        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           组           |    http://schemas.xmlsoap.org/claims/Group     |

必须仅发送一个采用合适格式的名称 ID 声明。 满足该条件时，还可能会发送许多其他声明（假设它们符合表中描述的限制）。

> [!NOTE]
> AD FS 1。*x*联合身份验证服务只能解释以的统一资源标识符 URI 开头的传入声明类型 \( \) http://schemas.xmlsoap.org/claims/ 。

## <a name="see-also"></a>另请参阅
[Windows Server 2012 中的 AD FS 设计指南](AD-FS-Design-Guide-in-Windows-Server-2012.md)
