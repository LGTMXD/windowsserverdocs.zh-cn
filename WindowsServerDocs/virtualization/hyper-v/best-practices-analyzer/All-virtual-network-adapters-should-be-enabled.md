---
title: 应启用所有虚拟网络适配器
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 450a3b42529be9a85991fcaf5263bae7b7827b1a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857830"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>应启用所有虚拟网络适配器

>适用于：Windows Server 2016


  
|属性|详细信息|  
|-|-|  
|**操作系统**|Windows Server 2016|  
|**产品/功能**|Hyper-V|  
|**对应**|警告|  
|**类别**|配置|  
  
在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。  
  
## <a name="issue"></a>问题  
  
*在管理操作系统中禁用了与物理网络适配器关联的一个或多个虚拟网络适配器。*  
  
## <a name="impact"></a>影响  
  
*此服务器的配置不是最佳的。*  
  
管理操作系统无法使用此计算机上的一个物理网络适配器连接到物理（外部）网络，因为它与已禁用的虚拟网络适配器相关联。  
  
## <a name="resolution"></a>分辨率  
  
*使用网络 & Internet 设置来启用虚拟网络适配器。或者，使用虚拟交换机管理器重新配置外部虚拟交换机，使其不与管理操作系统共享。*  
  


