---
title: 启用为虚拟机配置的所有虚拟网络适配器
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 79971ff503afcc1a087aced579e30989233c2b4a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861960"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>启用为虚拟机配置的所有虚拟网络适配器

>适用于：Windows Server 2016

有关最佳实践和扫描的详细信息，请参阅 [最佳实践分析程序](https://go.microsoft.com/fwlink/?LinkId=122786)。  
  
|属性|详细信息|  
|-|-|  
|**操作系统**|Windows Server 2016|  
|**产品/功能**|Hyper-V|  
|**对应**|警告|  
|**类别**|配置|  
  
在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。  
  
## <a name="issue"></a>问题  
  
*可能在虚拟机中禁用了一个或多个网络适配器。*  
  
## <a name="impact"></a>影响  
  
*以下虚拟机可能不具有网络连接：*  
  
虚拟机名称 \<列表 >  
  
## <a name="resolution"></a>分辨率  
  
*使用来宾操作系统中的设备管理器来启用所有虚拟网络适配器。如果适配器不是必需的，请使用 Hyper-v 管理器将其从虚拟机中删除。*  
  


