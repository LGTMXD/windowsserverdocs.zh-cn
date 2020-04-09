---
title: 配置 DirectAccess 群集 NLB 测试实验室的步骤
description: 本主题是测试实验室指南的一部分-使用 windows Server 2016 的 Windows NLB 在群集中演示 DirectAccess
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: e508d3ee-ffa6-463f-a3dd-9e35e745c005
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c4f683cd9745bdb61ee95d89bcfc37622a4acf2c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853010"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>配置 DirectAccess 群集 NLB 测试实验室的步骤

>适用于：Windows Server（半年频道）、Windows Server 2016

以下步骤介绍了如何配置远程访问基础结构、配置远程访问服务器和客户端，以及如何通过 Internet 和 Homenet 子网测试 DirectAccess 连接。  
  
在本测试实验室指南中，你将通过执行以下步骤来构建网络负载平衡（NLB）启用的远程访问群集：  
  
-   [步骤1：完成 DirectAccess 配置](STEP-1-Complete-the-DirectAccess-Configuration.md)。 完成[测试实验室指南：演示带有混合 IPv4 和 IPv6 的 DirectAccess 单服务器安装程序](https://go.microsoft.com/fwlink/p/?LinkId=237004)中的所有步骤。  
  
-   [步骤2：配置 EDGE1](STEP-2-Configure-EDGE1.md)。 在 EDGE1 上配置远程访问角色以实现负载平衡。  
  
-   [步骤3：安装和配置 EDGE2](STEP-3-Install-and-Configure-EDGE2.md)。 EDGE2 充当远程访问群集中的第二个远程访问服务器。  
  
-   [步骤4：创建网络负载平衡远程访问群集](STEP-4-Create-the-Network-Load-Balanced-Remote-Access-Cluster.md)-EDGE1 配置为远程访问群集中的第一个服务器。 EDGE2 加入群集，并为群集配置 NLB。  
  
-   [步骤5：从 Internet 和群集测试 DirectAccess 连接](STEP-5-Test-DirectAccess-Connectivity-from-the-Internet-and-Through-the-Cluster.md)。 NLB 和群集配置完成后，可以通过负载平衡群集测试 DirectAccess 客户端连接。  
  
-   [步骤6：从 NAT 设备后面测试 DirectAccess 客户端连接](STEP-6-Test-DirectAccess-Client-Connectivity-from-Behind-a-NAT-Device.md)。 将客户端计算机移动到 NAT 设备后面，以模拟从主路由器后面测试 DirectAccess 客户端连接。  
  
-   [步骤7：在返回到公司网络时测试连接性](STEP-7-Test-Connectivity-When-Returning-to-the-Corpnet.md)。 确保客户端计算机在返回到公司资源时仍可访问公司资源。  
  
-   [步骤8：快照配置](da-cluster-nlb-s8-snapshot.md)。 完成测试实验室后，拍摄工作远程访问 NLB 群集的快照，以便稍后可将其返回到测试其他方案。  
  


