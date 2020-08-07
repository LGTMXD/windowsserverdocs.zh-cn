---
ms.assetid: f67b0bc9-e5af-4891-9da0-d9be539af42d
title: 确定 AD FS 部署拓扑
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: dfb863cf85f9e9bffadbe10ca017491341596dad
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972114"
---
# <a name="determine-your-ad-fs-deployment-topology"></a>确定 AD FS 部署拓扑

规划 Active Directory 联合身份验证服务 AD FS 的部署的第一步 \( \) 是确定正确的部署拓扑，以满足组织的单一登录 \- \( SSO \) 需求。 本节中的主题介绍可用于 AD FS 的各种部署拓扑。 这些主题还描述了与每个部署拓扑相关联的优势和限制，以便你可以为特定的业务需求选择最合适的拓扑。

在阅读本部署拓扑主题之前，我们建议你先按照下表中显示的顺序完成任务。

|建议的任务|说明|参考|
|--------------------|---------------|-------------|
|查看如何存储 AD FS 数据并将其复制到联合服务器场中的其他联合服务器。|了解存储在 AD FS 配置数据库中的基础数据的用途以及针对其使用的复制方法。 本主题介绍了配置数据库的概念，并描述了这两种数据库类型： Windows 内部数据库 \( WID \) 和 Microsoft SQL Server。|[AD FS 配置数据库的角色](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|
|选择将在你的组织中部署的 AD FS 配置数据库的类型。|查看与使用 WID 或 SQL Server 作为 AD FS 配置数据库相关联的各种优势和限制，以及它们所支持的各种应用程序方案。|[AD FS 部署拓扑注意事项](AD-FS-Deployment-Topology-Considerations.md)|

> [!NOTE]
> 若要实现基本冗余、负载平衡以及根据需要缩放联合身份验证服务的选项 \( \) ，我们建议你在所有生产环境中为每个联合服务器场至少部署两台联合服务器，而不考虑你将使用的数据库类型。

当你查看了上一个表中的内容后，请继续执行本部分中的以下主题：

-   [使用 WID 的独立联合服务器](Stand-Alone-Federation-Server-Using-WID.md)

-   [使用 WID 的联合服务器场](Federation-Server-Farm-Using-WID-2012.md)

-   [使用 WID 和代理的联合服务器场](Federation-Server-Farm-Using-WID-and-Proxies-2012.md)

-   [使用 SQL Server 的联合服务器场](Federation-Server-Farm-Using-SQL-Server-2012.md)

选择 AD FS 部署拓扑后，我们建议你查看[规划 AD FS 服务器容量](Planning-for-AD-FS-Server-Capacity.md)的主题，以确定需要部署以支持此拓扑的服务器的建议数目。

## <a name="see-also"></a>另请参阅
[Windows Server 2012 中的 AD FS 设计指南](AD-FS-Design-Guide-in-Windows-Server-2012.md)

