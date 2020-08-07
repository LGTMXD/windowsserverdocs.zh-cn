---
ms.assetid: f15c02d7-1cbd-4eba-a571-0ea34ab93ef4
title: 运行重复数据删除
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: f382d229458f27795c09e0377e0f0b23ef7b395b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936228"
---
# <a name="running-data-deduplication"></a>运行重复数据删除

> 适用于：Windows Server（半年频道）、Windows Server 2016

## <a name="running-data-deduplication-jobs-manually"></a><a id="running-dedup-jobs-manually"></a>手动运行重复数据删除作业

你可以使用以下 PowerShell cmdlet 手动运行每个预定的重复数据删除作业：
* [`Start-DedupJob`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12))：启动新的重复数据删除作业
* [`Stop-DedupJob`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12))：停止正在进行的重复数据删除作业 (或将其从队列中删除) 
* [`Get-DedupJob`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12))：显示所有活动和已排队的重复数据删除作业

[预定重复数据删除作业时可用的所有设置](advanced-settings.md#modifying-job-schedules-available-settings)也可在你手动启动作业时使用（排定特定的设置除外）。 例如，要手动启动具有高优先级、最大 CPU 使用率和最大内存使用量的[优化](understand.md#job-info-optimization)作业，请使用管理员特权执行以下 PowerShell 命令：

```PowerShell
Start-DedupJob -Type Optimization -Volume <Your-Volume-Here> -Memory 100 -Cores 100 -Priority High
```

## <a name="monitoring-data-deduplication"></a><a id="monitoring-dedup"></a>监控重复数据删除

### <a name="job-successes"></a><a id="monitoring-dedup-job-successes"></a>作业成功

由于重复数据删除使用后处理模型，因此，[重复数据删除作业](understand.md#job-info) 成功完成非常重要。 查看最近作业状态的一种简单方法是使用 [`Get-DedupStatus`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) PowerShell cmdlet。 定期检查以下字段：

* 对于[优化作业](understand.md#job-info-optimization)，请查看 `LastOptimizationResult` (0 = Success)、`LastOptimizationResultMessage` 和 `LastOptimizationTime`（应当为最新）。
* 对于[垃圾收集作业](understand.md#job-info-gc)，请查看 `LastGarbageCollectionResult` (0 = Success)、`LastGarbageCollectionResultMessage` 和 `LastGarbageCollectionTime`（应当为最新）。
* 对于[完整性清理作业](understand.md#job-info-scrubbing)，请查看 `LastScrubbingResult` (0 = Success)、`LastScrubbingResultMessage` 和 `LastScrubbingTime`（应当为最新）。

> [!Note]
> 在 Windows 事件查看器的 `\Applications and Services Logs\Windows\Deduplication\Operational` 下找到作业成功和失败的详细信息。

### <a name="optimization-rates"></a><a id="monitoring-dedup-optimization-rates"></a>优化速率

[优化作业](understand.md#job-info-optimization)失败的一个标志是呈下降趋势的优化比率，它可能指示优化作业跟不上更改或改动的速率。 可以使用 PowerShell cmdlet 检查优化速率 [`Get-DedupStatus`](/previous-versions/system-center/system-center-2012-R2/hh758173(v=sc.12)) 。

> [!Important]
> `Get-DedupStatus`具有两个与优化比率相关的字段： `OptimizedFilesSavingsRate` 和 `SavingsRate` 。 这两个都是要跟踪的重要值，但每个都具有独特的含义。
> - `OptimizedFilesSavingsRate`仅适用于 "策略中" () 的优化文件 `space used by optimized files after optimization / logical size of optimized files` 。
> - `SavingsRate`适用于整个卷 (`space used by optimized files after optimization / total logical size of the optimization`) 。

## <a name="disabling-data-deduplication"></a><a id="disabling-dedup"></a>禁用重复数据删除
若要关闭重复数据删除，请运行“[取消优化作业](understand.md#job-info-unoptimization)”。 要撤消卷优化，请运行以下命令：

```PowerShell
Start-DedupJob -Type Unoptimization -Volume <Desired-Volume>
```

> [!Important]
> 如果卷没有足够的空间来容纳未优化的数据，则取消优化作业将失败。

## <a name="frequently-asked-questions"></a><a id="faq"></a>常见问题
**是否有可用的 System Center Operations Manager 管理包来监控重复数据删除？**
是的。 可通过 System Center 文件服务器管理包监控重复数据删除。 有关详细信息，请参阅[文件服务器 2012 R2 的 System Center 管理包指南](https://download.microsoft.com/download/6/F/7/6F7A33B9-9383-48ED-9252-23C2C8AD1BDA/MPGuide_FileServer2012R2.doc)文档。
