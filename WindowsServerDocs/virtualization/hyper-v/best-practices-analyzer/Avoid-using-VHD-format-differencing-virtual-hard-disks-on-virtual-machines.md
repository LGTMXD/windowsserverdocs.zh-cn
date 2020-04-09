---
title: 避免在生产环境中运行服务器工作负荷的虚拟机上使用 VHD 格式的差异虚拟硬盘
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 272de33d-2708-4679-8564-ee28848a2839
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: a11959266db4c9f3da73123c41a211198f27b9a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857720"
---
# <a name="avoid-using-vhd-format-differencing-virtual-hard-disks-on-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>避免在生产环境中运行服务器工作负荷的虚拟机上使用 VHD 格式的差异虚拟硬盘

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
*一个或多个虚拟机使用 VHD 格式的差异虚拟硬盘。*  
  
## <a name="impact"></a>**对**  
*如果出现电源故障，VHD 格式差异虚拟硬盘可能会出现一致性问题。如果物理磁盘在发生电源故障时要修改的 .vhd 文件中的扇区执行不完整或不正确的更新，则会发生一致性问题。这会影响以下虚拟机：*  
  
虚拟机 \<列表 >  
  
## <a name="resolution"></a>**解决方法**  
*关闭虚拟机并将 VHD 格式差异虚拟硬盘链转换为 VHDX 格式，或者将该链合并为固定的虚拟硬盘。（VHDX 格式具有可靠性机制，可帮助防止磁盘因电源故障而损坏。）但是，如果在某个时间点可能会将虚拟硬盘附加到早期版本的 Windows，请不要转换虚拟硬盘。Windows Server 2012 之前的 windows 版本不支持 VHDX 格式。*  
  


