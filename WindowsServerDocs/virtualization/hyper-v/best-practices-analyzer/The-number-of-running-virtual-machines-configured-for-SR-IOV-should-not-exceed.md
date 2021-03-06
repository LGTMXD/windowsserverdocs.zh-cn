---
title: 为 SR-IOV 配置的正在运行的虚拟机的数量不应超过可供虚拟机使用的虚拟功能的数目
description: 此最佳做法分析器规则文本的联机版本。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 16126118cdbf2341059fb0871ee7c33b62dc6b94
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960380"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>为 SR-IOV 配置的正在运行的虚拟机的数量不应超过可供虚拟机使用的虚拟功能的数目

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[运行最佳做法分析器扫描并管理扫描结果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。

|属性|详细信息|
|-|-|
|**操作系统**|Windows Server 2016|
|**产品/功能**|Hyper-V|
|**严重性**|警告|
|**类别**|配置|

在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。

## <a name="issue"></a>问题
*没有足够的虚拟功能可用来容纳为 (SR-IOV) 的单根 i/o 虚拟化配置的正在运行的虚拟机数。*

## <a name="impact"></a>影响
*在以下虚拟机上，网络性能可能不是最佳的：*

\<list of virtual machines>

## <a name="resolution"></a>解决方法
*请考虑在不需要 SR-IOV 虚拟功能的一个或多个虚拟机上禁用 SR-IOV。*



