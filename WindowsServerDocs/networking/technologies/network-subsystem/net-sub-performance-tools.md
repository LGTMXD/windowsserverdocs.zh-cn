---
title: 用于网络工作负荷的性能工具
description: 本主题是 Windows Server 2016 的网络子系统性能优化指南的一部分。
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: dcscontentpm
ms.author: v-tea
author: Teresa-Motiv
ms.date: 07/16/2018
ms.openlocfilehash: 3e08541b1bfd6dd07d134560c9d03306566b18db
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953913"
---
# <a name="performance-tools-for-network-workloads"></a>用于网络工作负荷的性能工具

>适用于：Windows Server（半年频道）、Windows Server 2016

您可以使用本主题来了解性能工具。

本主题包含有关客户端到服务器流量工具、TCP/IP 窗口大小和 Microsoft Server 性能顾问的部分。

##  <a name="client-to-server-traffic-tool"></a><a name="bkmk_tuning"></a>客户端到服务器流量工具

通过客户端到服务器的流量 \( ctsTraffic \) 工具，可以创建和验证网络流量。

有关详细信息并下载该工具，请参阅[ctsTraffic (客户端到服务器的通信) ](https://github.com/Microsoft/ctsTraffic)。

##  <a name="tcpip-window-size"></a><a name="bkmk_size"></a>TCP/IP 窗口大小

对于 1 GB 适配器，上表中显示的设置应能提供良好的吞吐量，因为 NTttcp 将默认的 TCP 窗口大小设置为 64 K，通过特定的逻辑处理器选项 \( SO_RCVBUF \) 来连接。 这为低延迟网络提供了良好的性能。

与此相反，对于高延迟网络或 10 GB 适配器，NTttcp 的默认 TCP 窗口大小值产生的性能低于最佳性能。 在这两种情况下，都必须调整 TCP 窗口大小，以允许更大的带宽延迟产品。

可以使用 **-rb**选项将 TCP 窗口大小静态设置为较大的值。 此选项将禁用 TCP 窗口自动优化，建议仅在用户完全了解 TCP/IP 行为中的结果更改时才使用此选项。 默认情况下，TCP 窗口大小设置为足够的值，并且仅在繁重的负载下或通过高延迟的链接进行调整。

##  <a name="microsoft-server-performance-advisor"></a><a name="bkmk_advisor"></a>Microsoft Server 性能顾问

Microsoft Server Performance Advisor \( SPA \) 可帮助 IT 管理员收集指标来识别、比较和诊断 windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 R2 或 windows server 2008 部署中的潜在性能问题。

SPA 生成全面的诊断报告和图表，并提供建议来帮助你快速分析问题和制定纠正措施。

 有关详细信息和下载顾问，请参阅 Windows 硬件开发人员中心中的[Microsoft Server Performance advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) 。

有关本指南中的所有主题的链接，请参阅[网络子系统性能优化](net-sub-performance-top.md)。