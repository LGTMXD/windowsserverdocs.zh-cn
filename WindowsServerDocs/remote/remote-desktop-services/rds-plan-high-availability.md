---
title: 远程桌面服务 - 高可用性
description: 有关设置高可用性 RDS 部署的规划信息。
ms.topic: article
ms.assetid: ec630ea0-ab80-4dfe-a25f-f4f601651f72
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: c50c66bee8f9f387497ef2f5971dbee5e1b402c6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955004"
---
# <a name="remote-desktop-services---high-availability"></a>远程桌面服务 - 高可用性

>适用于：Windows Server（半年频道）、Windows Server 2019、Windows Server 2016

在大型系统中，故障和限制不可避免。 可以很轻松地设置远程桌面基础结构角色来支持高可用性，并使最终用户每次都能顺利地建立连接。

在远程桌面服务中，以下各项代表远程桌面基础结构角色，并随附了建立高可用性的指导：
- [远程桌面连接代理](./rds-connection-broker-cluster.md)
- [远程桌面网关](./rds-rdweb-gateway-ha.md)
- 远程桌面授权
- [远程桌面 Web 访问](./rds-rdweb-gateway-ha.md)

通过在另一台计算机上复制每个角色服务来建立高可用性。 在 Azure 中，在可用性集中放置两个虚拟机（托管相同的角色）可以获得有保证的运行时间。

除了可用性集以外，现在还可以利用 Azure SQL 数据库的强大功能及其 Azure 保障的 SLA，来确保始终能够获得连接信息，并可将用户重定向到其桌面和应用程序。

有关创建 RDS 环境的最佳做法，请参阅[桌面托管体系结构](desktop-hosting-reference-architecture.md)。
