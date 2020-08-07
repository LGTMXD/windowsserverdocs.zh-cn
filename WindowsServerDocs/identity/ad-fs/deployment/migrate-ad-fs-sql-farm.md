---
title: 迁移 AD FS 2.0 联合服务器 SQL 场
description: 提供有关将 AD FS 2.0 server SQL 场迁移到 Windows Server 2012 的信息
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: f63a797a30d363b8662dfcc6bfcac46f79dc3eb0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938196"
---
# <a name="migrate-an-ad-fs-20-sql-farm"></a>迁移 AD FS 2.0 SQL 场
本文档详细介绍了如何将 AD FS 2.0 SQL 场迁移到 Windows Server 2012。


## <a name="migrate-a-sql-server-farm"></a>迁移 SQL Server 场
 若要将 SQL Server 场迁移到 Windows Server 2012，请执行以下步骤：

1.  对于 SQL Server 场中的每个服务器，请查看并执行[迁移 SQL Server 场](prepare-to-migrate-a-sql-server-farm.md)中的过程。

2.  从负载平衡器中删除你的 SQL Server 场中的任何服务器。

3.  将 SQL Server 场中此服务器上的操作系统从 Windows Server 2008 R2 或 Windows Server 2008 升级到 Windows Server 2012。 有关详细信息，请参阅[安装 Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11))。

> [!IMPORTANT]
>  作为操作系统升级的结果，在此服务器上的 AD FS 配置将丢失并且 AD FS 2.0 的服务器角色会被删除。 改为安装 Windows Server 2012 AD FS Server 角色，但未对其进行配置。 你必须手动创建原始 AD FS 配置并还原剩余的 AD FS 设置，以完成联合服务器迁移。

4. 在你的 SQL Server 场中的此服务器上创建原始 AD FS 配置，通过使用 AD FS Windows PowerShell cmdlet 将服务器添加到现有的场。

> [!IMPORTANT]
>  如果使用 SQL Server 来存储你的 AD FS 配置数据库，则必须使用 Windows PowerShell 创建原始 AD FS 配置。

  - 打开 Windows PowerShell，并运行如下命令： `$fscredential = Get-Credential`。
  - 输入你在为迁移准备 SQL Server 场时所记录的服务帐户的名称和密码。
  - 运行以下命令： `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`，其中 `Data Source` 是以下文件 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`的策略存储连接字符串值中的数据源值。

5. 将刚刚升级到 Windows Server 2012 的服务器添加到负载均衡器。

6. 对于你的 SQL Server 场中的剩余节点，重复步骤 2 到 6。

7. 当 SQL Server 场中的所有服务器升级到 Windows Server 2012 时，还原任何剩余的 AD FS 自定义项，如自定义属性存储。

## <a name="next-steps"></a>后续步骤
 [准备迁移 AD FS 2.0 联合服务器](prepare-to-migrate-ad-fs-fed-server.md)[准备迁移 AD FS 2.0 联合服务器代理](prepare-to-migrate-ad-fs-fed-proxy.md)[迁移 AD FS 2.0 联合服务器](migrate-the-ad-fs-fed-server.md)迁移[AD FS 2.0 联合服务器代理](migrate-the-ad-fs-2-fed-server-proxy.md)[迁移 AD FS 1.1 Web 代理](migrate-the-ad-fs-web-agent.md)
