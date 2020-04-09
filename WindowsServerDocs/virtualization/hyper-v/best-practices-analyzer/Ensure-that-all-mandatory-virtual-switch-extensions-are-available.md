---
title: 确保所有必需的虚拟交换机扩展可用
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 14c9fc31521a7d4f5e0eed821c0cc49dcfe74e69
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861930"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>确保所有必需的虚拟交换机扩展可用

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[运行最佳做法分析器扫描并管理扫描结果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。  
  
|属性|详细信息|  
|-|-|  
|**操作系统**|Windows Server 2016|  
|**产品/功能**|Hyper-V|  
|**对应**|警告|  
|**类别**|配置|  
  
在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。  
  
## <a name="issue"></a>问题  
*一个或多个虚拟网络适配器已连接到具有已禁用或未安装的必需扩展的虚拟交换机。*  
  
## <a name="impact"></a>影响  
*在以下虚拟机上的一个或多个虚拟网络适配器上阻止网络流量：*  
  
虚拟机 \<列表 >  
  
## <a name="resolution"></a>分辨率  
*首先，请确保已在主机上安装了强制扩展，并在必要时安装扩展。然后，如果强制扩展被禁用，请使用虚拟交换机管理器或 Windows PowerShell cmdlet VMSwitchExtension 来启用该扩展。*  
  


