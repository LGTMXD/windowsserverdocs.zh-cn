---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: 计算机命名
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2b396778b458976604e527fad0c4649d03239fa6
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624375"
---
# <a name="computer-naming"></a>计算机命名

> 适用于：Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

当运行 Windows 2000、Windows XP、Windows Server 2003、Windows Server 2008 或 Windows Vista 操作系统的计算机加入域时，默认情况下，计算机会为自己分配一个名称。 它自己分配的名称包含计算机的主机名（即 "系统属性" 中的计算机名称）以及计算机加入的 Active Directory 域的域名系统（DNS）名称（即 "系统属性" 中的主 DNS 后缀）。 主机名和域名的 DNS 名称的串联称为完全限定的域名（FQDN）。 例如，如果主机名为 Server1 的计算机加入域 corp.contoso.com，则计算机的 FQDN 为 server1.corp.contoso.com。

如果计算机已有一个不同的 DNS 域名，该域名静态地输入到 DNS 区域或由集成的 DNS/动态主机配置协议（DHCP）服务器服务进行注册，则该计算机的 FQDN 与先前注册的名称不同。 计算机可以通过任一名称引用。

有关 Active Directory 域服务（AD DS）中的命名约定的详细信息，请参阅[Active Directory 中的计算机、域、站点和 ou 的命名约定](https://support.microsoft.com/help/909264/)。
