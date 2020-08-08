---
title: 应配置使用虚拟光纤通道适配器配置的虚拟机以实现基于光纤通道的存储的高可用性
description: 此最佳做法分析器规则文本的联机版本。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 60a96d6e559f3fefe6f8c1c52c2d145efa006c99
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960180"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>应配置使用虚拟光纤通道适配器配置的虚拟机以实现基于光纤通道的存储的高可用性

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[运行最佳做法分析器扫描并管理扫描结果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。

|属性|详细信息|
|-|-|
|**操作系统**|Windows Server 2016|
|**产品/功能**|Hyper-V|
|**严重性**|信息|
|**类别**|配置|

在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。

## <a name="issue"></a>**问题**
*一台或多台虚拟机缺少与基于光纤通道的存储的高度可用连接，因为这些虚拟机配置了仅连接到一个主机总线适配器 (HBA) 的虚拟光纤通道适配器。*

## <a name="impact"></a>**影响**
*如果主机总线适配器出现故障，则可能会阻止存储和虚拟机之间的光纤通道连接。这会影响以下虚拟机：*

\<list of virtual machines>

## <a name="resolution"></a>**解决方法**
*添加从虚拟机到主机总线适配器的另一个连接，并在来宾操作系统中配置多路径 i/o (MPIO) 以建立冗余的光纤通道连接。*



