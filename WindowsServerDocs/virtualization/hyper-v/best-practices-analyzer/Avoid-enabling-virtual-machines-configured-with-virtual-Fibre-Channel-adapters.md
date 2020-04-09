---
title: 如果目标上的逻辑单元（Lun）光纤通道的路径更少，请避免启用虚拟光纤通道适配器配置的虚拟机以允许实时迁移。
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 7989d2e1908f6be32f4661900fc507b5843b55c9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857770"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>如果目标上的逻辑单元（Lun）光纤通道的路径更少，请避免启用虚拟光纤通道适配器配置的虚拟机以允许实时迁移。

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[运行最佳做法分析器扫描并管理扫描结果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。  
  
|属性|详细信息|  
|-|-|  
|**操作系统**|Windows Server 2016|  
|**产品/功能**|Hyper-V|  
|**对应**|警告|  
|**类别**|配置|

在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。
  
## <a name="issue"></a>**问题**  
*一台或多台虚拟机的虚拟化 WMI 提供程序中设置了 AllowReducedFcRedunancy 属性。*  
  
## <a name="impact"></a>**对**  
*以下虚拟机的实时迁移可能会导致存储的数据丢失或中断 i/o：*  
  
虚拟机 \<列表 >  
  
## <a name="resolution"></a>**解决方法**  
*请考虑清除受影响的虚拟机上的 AllowReducedFcRedundancy WMI 属性。如果清除此属性，则可以在使用虚拟光纤通道适配器配置的虚拟机上执行实时迁移，只在目标上要光纤通道的路径数等于或大于源上的路径数时。这些检查可帮助防止数据丢失或存储中断中断。* 