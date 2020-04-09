---
title: 解决 vRSS 问题
description: 如果看不到 vRSS 负载平衡到 VM LPs 的流量，请解决 vRSS 问题。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/04/2018
ms.openlocfilehash: 1caedfcc5711df98836b3d373ebf4384fa1c7469
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858040"
---
# <a name="resolve-vrss-issues"></a>解决 vRSS 问题

如果已完成所有准备步骤，但仍未看到 vRSS 负载平衡向 VM LPs 的流量，则可能存在不同的问题。

1. 执行准备步骤之前，已禁用了 vRSS，必须启用。 可以运行**VMNetworkAdapter**来为 VM 启用 vRSS。

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. 已在 VM 或主机 vNIC 上禁用 RSS。 默认情况下，Windows Server 2016 启用 RSS;有人可能已将其禁用。 

   - Enabled = **True**

   **查看当前设置：** 

   在 vm 中的 vRSS\(中运行以下 PowerShell cmdlet\) 或在 host vNIC vRSS\)主机 \(上运行。

   ```PowerShell
   Get-NetAdapterRss
   ```

   **启用此功能：** 

   若要将值从 False 更改为 True，请运行以下 PowerShell cmdlet。

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   另一种用于配置 RSS 的系统范围的方法是使用 netsh。 使用 
   
    ```cmd
   netsh int tcp show global
   ```
   
   确保未全局禁用 RSS。 并在必要时启用它。 此设置不会被 *-Get-netadapterrss 所涉及。

3. 如果在配置 vRSS 后发现 VMMQ 未启用，请在每个连接到虚拟交换机的适配器上验证以下设置：

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **True**

   ![vmmq-已启用](../../media/vmmq-enabled.png)

   **查看当前设置：** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **启用此功能：** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _（Windows Server 2019）_ 将**VrssQueueSchedulingMode**设置为**动态**时，不能启用 VMMQ （VmmqEnabled = False）。 启用 VMMQ 后，VrssQueueSchedulingMode 不会更改为动态。<p>启用 VMMQ 后，**动态** **VrssQueueSchedulingMode**需要驱动程序支持。  VMMQ 是对逻辑处理器上的数据包位置的卸载，因此需要驱动程序支持才能利用动态算法。  请安装 NIC 供应商的驱动程序和支持动态 VMMQ 的固件。



---
