---
title: 配置了基于证书的身份验证，但未在副本服务器或故障转移群集节点上安装指定的证书
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: cc89aa201de4b25e4c221b770e6f88908785c859
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857680"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>配置了基于证书的身份验证，但未在副本服务器或故障转移群集节点上安装指定的证书

>适用于：Windows Server 2016


  
有关*最佳做法和扫描的详细信息，请参阅*[最佳做法分析器](https://go.microsoft.com/fwlink/?LinkId=122786)。  
  
|属性|详细信息|  
|-|-|  
|**操作系统**|Windows Server 2016|  
|**产品/功能**|Hyper-V|  
|**对应**|错误|  
|**类别**|配置|  

在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。

## <a name="issue"></a>问题  
  
*副本服务器（或任何故障转移群集节点）上未安装用于提供基于证书的复制的 Hyper-v 副本所配置的安全证书。*  
  
## <a name="impact"></a>影响  
  
*发生群集故障转移或移动到其他节点时，如果新节点还没有安装适当的证书，Hyper-v 复制将暂停。这会影响以下节点：*  
  
\<节点列表 >  
  
## <a name="resolution"></a>分辨率  
  
*在副本服务器上安装配置的证书（以及故障转移群集中的所有关联节点（如果有）。*  
  


