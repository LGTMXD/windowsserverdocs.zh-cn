---
ms.assetid: 5b5bab7a-727b-47ce-8efa-1d37a9639cba
title: 虚拟机负载平衡深入探讨
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: cebdc8c192abd737478c3b7a0c3db3e4a2bc8091
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957144"
---
# <a name="virtual-machine-load-balancing-deep-dive"></a>虚拟机负载平衡深入探讨

> 适用于：Windows Server 2019、Windows Server 2016

[虚拟机负载平衡功能](vm-load-balancing-overview.md)优化了故障转移群集中节点的利用率。 本文档介绍如何配置和控制 VM 负载平衡。

## <a name="heuristics-for-balancing"></a><a id="heuristics-for-balancing"></a>用于平衡的试探法
虚拟机负载平衡基于以下试探法评估节点的负载：
1. 当前**内存压力**：内存是 hyper-v 主机上最常见的资源约束
2. 在5分钟时间范围内平均节点的 CPU**利用率**：减少群集中的节点变得过度提交

## <a name="controlling-the-aggressiveness-of-balancing"></a><a id="controlling-aggressiveness-of-balancing"></a>控制平衡的入侵
可以使用群集通用属性 "AutoBalancerLevel" 配置基于内存和 CPU 试探法的平衡。 若要控制入侵，请在 PowerShell 中运行以下内容：

```PowerShell
(Get-Cluster).AutoBalancerLevel = <value>
```

| AutoBalancerLevel | 入侵 | 行为 |
|-------------------|----------------|----------|
| 1（默认值） | 低 | 当主机超过80% 时移动 |
| 2 | 中型 | 当主机超过70% 时移动 |
| 3 | 高 | 平均节点并在主机高于平均5% 时移动 |

![配置入侵平衡的 PowerShell 图形](media/vm-load-balancing/detailed-VM-load-balancing-1.jpg)

## <a name="controlling-vm-load-balancing"></a>控制 VM 负载均衡
默认情况下，VM 负载平衡处于启用状态，并且当负载平衡发生时，可以通过群集公用属性 "AutoBalancerMode" 进行配置。 控制节点公平平衡群集的时间：

### <a name="using-failover-cluster-manager"></a>使用故障转移群集管理器：
1. 右键单击群集名称，然后选择 "属性" 选项 ![ 图 "选择群集的属性" 故障转移群集管理器](media/vm-load-balancing/detailed-VM-load-balancing-2.jpg)

2.  选择 "均衡器" 窗格，选择 ![ 均衡器选项故障转移群集管理器](media/vm-load-balancing/detailed-VM-load-balancing-3.jpg)

### <a name="using-powershell"></a>使用 PowerShell：
运行以下内容：
```powershell
(Get-Cluster).AutoBalancerMode = <value>
```

|AutoBalancerMode |行为|
|:----------------:|:----------:|
|0| 已禁用|
|1| 节点联接的负载均衡|
|2（默认值）| 节点加入和每30分钟的负载均衡 |

## <a name="vm-load-balancing-vs-system-center-virtual-machine-manager-dynamic-optimization"></a>VM 负载平衡与 System Center Virtual Machine Manager 动态优化
节点公平功能提供内置功能，该功能面向部署，而无需 (SCVMM) System Center Virtual Machine Manager。 SCVMM 动态优化是用于平衡 SCVMM 部署的群集中虚拟机负载的建议机制。 启用动态优化后，SCVMM 会自动禁用 Windows Server VM 负载平衡。

## <a name="see-also"></a>另请参阅
* [虚拟机负载平衡概述](vm-load-balancing-overview.md)
* [故障转移群集](failover-clustering-overview.md)
* [Hyper-v 概述](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)
