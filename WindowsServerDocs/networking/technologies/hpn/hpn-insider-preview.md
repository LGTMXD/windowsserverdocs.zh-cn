---
title: Windows Server 2019 中的 HPN 功能的内部预览版
description: 了解 Windows Server 2019 中的新增高性能网络功能。
manager: dougkim
author: eross-msft
ms.author: lizross
ms.date: 09/12/2018
ms.topic: article
ms.openlocfilehash: 2eb6ec82d9127e89f1d7871d0143ae3716b4355e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955644"
---
# <a name="new-hpn-features-in-windows-server-2019"></a>Windows Server 2019 中的新 HPN 功能


## <a name="dynamic-vrss-and-vmmq"></a>动态 vRSS 和 VMMQ

>适用于：Windows Server 2019

过去，虚拟机队列和虚拟机多队列功能在网络吞吐量第一次到达10GbE 标记后，为单个 Vm 启用了更高的吞吐量。 遗憾的是，成功所需的规划、基线、优化和监视变成了一个大的任务;通常不是 IT 管理员想要花费的。

Windows Server 2019 通过根据需要动态分配和优化网络工作负荷的处理来改善这些优化。 Windows Server 2019 确保最高效率，并为 IT 管理员消除了配置负担。

有关详细信息，请参阅：

-   [公告博客](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-   [适用于 IT 专业人员的验证指南](https://aka.ms/DVMMQ-Validation)

## <a name="receive-segment-coalescing-rsc-in-the-vswitch"></a>在 vSwitch 中接收段合并 (RSC)

>适用于：Windows Server 2019 和 Windows 10 版本 1809

在 vSwitch 中 (RSC) 的接收段合并是一项增强功能，可在数据遍历 vSwitch 之前将多个 TCP 段合并为较大的段。 大段可改善虚拟工作负荷的网络性能。

以前，这是 NIC 实现的卸载。 遗憾的是，在将适配器连接到虚拟交换机时，此功能被禁用。 Windows Server 2019 和 Windows 10 2018 10 月版中的 vSwitch 中的 RSC 消除了这一限制。

默认情况下，在外部虚拟交换机上启用 vSwitch 中的 RSC。

有关详细信息，请参阅：

-  [公告博客](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-  [适用于 IT 专业人员的验证指南](https://aka.ms/RSC-Validation)
