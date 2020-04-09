---
title: 避免将一个存储路径映射到多个资源池
description: 此最佳做法分析器规则文本的联机版本。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 53ef04a2dde875b26dd109075a2cfa4484ebd5cd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857750"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>避免将一个存储路径映射到多个资源池

>适用于：Windows Server 2016

有关最佳做法和扫描的详细信息，请参阅[运行最佳做法分析器扫描并管理扫描结果](https://go.microsoft.com/fwlink/p/?LinkID=223177)。  
  
|属性|详细信息|  
|-|-|  
|**操作系统**|Windows Server 2016|  
|**产品/功能**|Hyper-V|  
|**对应**|警告|  
|**类别**|操作|  
  
在以下部分中，"斜体" 指示在此问题的最佳做法分析器工具中出现的 UI 文本。
  
## <a name="issue"></a>**问题**  
*存储文件路径映射到多个资源池。*  
  
## <a name="impact"></a>**对**  
*对于指定的存储池类型，以下父池和子池共享同一存储路径：*  
  
\<池列表 >  
  
## <a name="resolution"></a>**解决方法**  
*使用 Windows PowerShell 重新配置存储资源池，使多个池不会使用相同的存储路径。*  
  


