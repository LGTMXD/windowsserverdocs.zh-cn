---
title: 网络子系统性能调整
description: 本主题是 Windows Server 2016 的网络子系统性能优化指南的一部分。
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: dcscontentpm
ms.author: v-tea
author: Teresa-Motiv
ms.openlocfilehash: 40819f850788192f9057f8fd73c6c63f9d61dc0c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953903"
---
# <a name="network-subsystem-performance-tuning"></a>网络子系统性能调整

>适用于：Windows Server（半年频道）、Windows Server 2016

您可以使用本主题来概述网络子系统以及本指南中的其他主题的链接。

>[!NOTE]
>除了本主题之外，本指南的以下部分还提供了针对网络设备和网络堆栈的性能优化建议。
> - [选择网络适配器](net-sub-choose-nic.md)
> - [配置网络接口的顺序](net-sub-interface-metric.md)
> - [性能优化网络适配器](net-sub-performance-tuning-nics.md)
> - [与网络相关的性能计数器](net-sub-performance-counters.md)
> - [用于网络工作负荷的性能工具](net-sub-performance-tools.md)

性能优化网络子系统，特别是对于网络密集型工作负载，它可能涉及网络体系结构的每个层，也称为网络堆栈。 这些层大致分为以下几个部分。

1. **网络接口**。 这是网络堆栈中的最低层，其中包含与网络适配器直接通信的网络驱动程序。

2. **网络驱动程序接口规范 (NDIS) **。 NDIS 为其下面的驱动程序和其上的层（如协议堆栈）公开接口。

3. **协议堆栈**。 协议堆栈实现了协议，如 TCP/IP 和 UDP/IP。 这些层向其上方的层公开传输层接口。

4. **系统驱动程序**。 这些客户端通常使用传输数据扩展插件 (TDX) 或 Winsock 内核 (WSK) 接口，以向用户模式应用程序公开接口。 WSK 接口是在 Windows Server 2008 和 Windows Vista 中引入的 &reg; ，它通过 AFD.sys 公开。 接口通过消除用户模式和内核模式间的切换来提高性能。

5. **用户模式应用程序**。 这些通常是 Microsoft 解决方案或自定义应用程序。

下表提供了网络堆栈层的垂直图解，其中包括在每个层中运行的项的示例。

![网络堆栈层](../../media/Network-Subsystem/network-layers.jpg)

