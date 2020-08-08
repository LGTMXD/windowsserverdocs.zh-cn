---
title: DHCP 子网选择选项
description: 本主题提供有关 Windows Server 2016 中的动态主机配置协议 (DHCP) 的 DHCP 子网选择选项的信息。
manager: dougkim
ms.topic: get-started-article
ms.assetid: ca19e7d1-e445-48fc-8cf5-e4c45f561607
ms.author: lizross
author: eross-msft
ms.date: 08/17/2018
ms.openlocfilehash: 5b7a680c77ee7a9002f674d4fc0266c50551abcc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949230"
---
# <a name="dhcp-subnet-selection-options"></a>DHCP 子网选择选项

>适用于：Windows Server（半年频道）、Windows Server 2016

您可以使用本主题来了解有关新的 DHCP 子网选择选项的信息。

DHCP 现在支持选项 82 \( 子选项 5 \) 。 你可以使用这些选项，允许 DHCP 代理客户端和中继代理请求特定子网的 IP 地址，并从特定的 IP 地址范围和范围请求 IP 地址。  有关更多详细信息，请参阅适用于[DHCPv4 的中继代理信息选项](https://tools.ietf.org/html/rfc3527)的**选项82子选项 5**： RFC 3527 链接选择子选项。

如果你使用的是配置了 DHCP 选项82、子选项5的 DHCP 中继代理，则中继代理可以从特定 IP 地址范围为 DHCP 客户端请求 IP 地址租约。


## <a name="option-82-sub-option-5-link-selection-sub-option"></a>选项82子选项5：链接选择子选项

中继代理链接选择子选项允许 DHCP 中继代理指定 DHCP 服务器应该从中分配 IP 地址和选项的 IP 子网。

通常，DHCP 中继代理依赖于网关 IP 地址 \( GIADDR \) 字段来与 DHCP 服务器进行通信。 但是，GIADDR 受其两个操作函数的限制：

1. 向 DHCP 服务器通知请求 IP 地址租约的 DHCP 客户端所在的子网。
2. 通知 DHCP 服务器要使用的 IP 地址以与中继代理通信。

在某些情况下，中继代理用于与 DHCP 服务器通信的 IP 地址可能不同于需要从其分配 DHCP 客户端 IP 地址的 IP 地址范围。

选项82的 "链接选择" 子选项在这种情况下非常有用，这允许中继代理显式声明其所需的子网，以 DHCP v4 选项82子选项5的形式分配 IP 地址。

> [!NOTE]
>
>  (GIADDR) 的所有中继代理 IP 地址都必须是活动 DHCP 作用域 IP 地址范围的一部分。 DHCP 作用域 IP 地址范围外的任何 GIADDR 都被认为是一种欺诈中继，Windows DHCP 服务器将不会确认来自这些中继代理的 DHCP 客户端请求。
>
> 可以为 "授权" 中继代理创建一个特殊的作用域。 创建包含 GIADDR (的作用域，如果 GIADDR 是连续 IP 地址) ，则从分发中排除 GIADDR 地址 (es) ，然后激活作用域。 这将授权中继代理，同时阻止分配 GIADDR 地址。


### <a name="use-case-scenario"></a>用例场景

在这种情况下，组织网络包括 DHCP 服务器和来宾用户的无线接入点 \( AP \) 。 来宾客户端 IP 地址是从组织 DHCP 服务器分配的-但是，由于防火墙策略限制，DHCP 服务器无法通过 broadcase 消息访问来宾无线网络或无线客户端。

若要解决此限制，请将 AP 配置为链接选择项选项5，以指定要从中为来宾客户端分配 IP 地址的子网，而在 GIADDR 中还指定了导致企业网络的内部接口的 IP 地址。
