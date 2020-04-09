---
title: 避免在动态虚拟硬盘或差异磁盘上的虚拟块与物理磁盘扇区之间出现对齐不一致
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 3f090f015f2179ba372e56d580477ef8d72d977f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857800"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>避免在动态虚拟硬盘或差异磁盘上的虚拟块与物理磁盘扇区之间出现对齐不一致

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
*检测到一个或多个虚拟硬盘出现对齐不一致问题。*  
  
### <a name="impact"></a>影响  
*如果虚拟硬盘存储在扇区大小为4K 的物理磁盘上，则使用虚拟硬盘的虚拟机或应用程序可能会遇到性能问题。这会影响以下虚拟机：*  
  
虚拟机 \<列表 >  
  
## <a name="resolution"></a>分辨率  
*使用 "创建虚拟硬盘向导" 来创建新的 VHD 格式或 VHDX 格式的虚拟硬盘，并将现有的虚拟硬盘指定为源磁盘。将创建新的虚拟硬盘，并在虚拟机块和物理磁盘之间进行对齐。*  
  


