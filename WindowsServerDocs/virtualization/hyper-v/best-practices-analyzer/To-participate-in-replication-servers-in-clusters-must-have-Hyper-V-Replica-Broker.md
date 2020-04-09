---
title: 若要参与复制，故障转移群集中的服务器必须配置 Hyper-v 副本代理
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 921d31aa63bcaaf0946c487d327144f5e29bcfe0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854580"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>若要参与复制，故障转移群集中的服务器必须配置 Hyper-v 副本代理

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[运行最佳做法分析器扫描并管理扫描结果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。  
  
|属性|详细信息|  
|-|-|  
|**操作系统**|Windows Server 2016|  
|**产品/功能**|Hyper-V|  
|**对应**|错误|  
|**类别**|配置|  
  
在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。  
  
## <a name="issue"></a>问题  
*对于故障转移群集，Hyper-v 副本需要使用 Hyper-v 副本代理名称，而不是单独的服务器名称。*  
  
## <a name="impact"></a>影响  
*如果将虚拟机移动到其他故障转移群集节点，复制将无法继续。*  
  
## <a name="resolution"></a>分辨率  
*使用故障转移群集管理器配置 Hyper-v 副本代理。在 "Hyper-v 管理器" 中，确保复制配置使用 Hyper-v 副本代理名称作为服务器名称。*  
  


