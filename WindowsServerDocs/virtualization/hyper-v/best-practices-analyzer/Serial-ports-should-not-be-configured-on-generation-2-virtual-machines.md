---
title: 不应在第2代虚拟机上配置串行端口
description: 此最佳做法分析器规则文本的联机版本。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b842adcb098a76edc6c42020dd87f8f3e224d9bd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938976"
---
# <a name="serial-ports-should-not-be-configured-on-generation-2-virtual-machines"></a>不应在第2代虚拟机上配置串行端口

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[运行最佳做法分析器扫描并管理扫描结果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。

|属性|详细信息|
|-|-|
|**操作系统**|Windows Server 2016|
|**产品/功能**|Hyper-V|
|**严重性**|警告|
|**类别**|配置|

在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。

## <a name="issue"></a>**问题**
*一个或多个第2代虚拟机配置了串行端口。*

## <a name="impact"></a>**影响**
*对于下列虚拟机，性能可能会受到影响：*

\<list of virtual machines>

## <a name="resolution"></a>**解决方法**
*如果这是有意的，则无需执行其他操作。否则，请考虑使用 Hyper-v 管理器或 Windows PowerShell 从虚拟机上的串行端口中删除连接字符串。*



