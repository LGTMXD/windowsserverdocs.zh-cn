---
title: 启用为虚拟机配置的所有虚拟网络适配器
description: 此最佳做法分析器规则文本的联机版本。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 7958bf5ced635c344ded45f8fde54bd7779ccbe9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960570"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>启用为虚拟机配置的所有虚拟网络适配器

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[最佳做法分析器](https://go.microsoft.com/fwlink/?LinkId=122786)。

|属性|详细信息|
|-|-|
|**操作系统**|Windows Server 2016|
|**产品/功能**|Hyper-V|
|**严重性**|警告|
|**类别**|配置|

在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。

## <a name="issue"></a>问题

*可能在虚拟机中禁用了一个或多个网络适配器。*

## <a name="impact"></a>影响

*以下虚拟机可能不具有网络连接：*

\<list of virtual machine names>

## <a name="resolution"></a>解决方法

*使用来宾操作系统中的设备管理器来启用所有虚拟网络适配器。如果适配器不是必需的，请使用 Hyper-v 管理器将其从虚拟机中删除。*



