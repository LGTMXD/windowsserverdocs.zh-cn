---
title: 用于 RSS 和 vRSS 的 Windows PowerShell 命令
description: 在本主题中，你将了解如何快速找到有关接收方缩放 (RSS) 和虚拟 RSS (vRSS) 的技术参考信息。
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/05/2018
ms.openlocfilehash: 424344147ff926694709aa60fbf57380fbbf665b
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996403"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>用于 RSS 和 vRSS 的 Windows PowerShell 命令

>适用于：Windows Server（半年频道）、Windows Server 2016

在本主题中，你将了解如何快速查找有关接收方缩放 \( RSS \) 和虚拟 RSS VRSS 的 Windows PowerShell 命令的技术参考信息 \( \) 。

使用以下 RSS 命令在具有多个处理器或多个内核的物理计算机上配置 RSS。 你可以使用相同的命令在 \( 运行受支持的操作系统的虚拟机 VM 上配置 vRSS \) 。 有关详细信息，请参阅[Windows PowerShell 中的网络适配器 cmdlet](/powershell/module/netadapter/?view=win10-ps)。

## <a name="configure-vmq"></a>配置 VMQ

vRSS 需要启用并配置 VMQ。 你可以使用以下 Windows PowerShell 命令来管理 VMQ 设置。

- [Get-netadaptervmq](/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Get-netadaptervmq](/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get-netadaptervmq](/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Get-netadaptervmq](/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## <a name="enable-and-configure-rss-on-a-native-host"></a>在本机主机上启用并配置 RSS

使用以下 PowerShell 命令在本机主机上配置 RSS，并在 VM 或主机虚拟 NIC 上管理 RSS (vNIC) 。 这些命令的某些参数可能还会影响 \( \) hyper-v 主机中虚拟机队列 VMQ。

>[!IMPORTANT]
>若要启用和使用 vRSS，请在 VM 或主机 vNIC 上启用 RSS。

- [Get-netadapterrss](/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Get-netadapterrss](/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get-netadapterrss](/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Get-netadapterrss](/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>在 Hyper-v \- 虚拟交换机端口上启用 vRSS

除了启用 VM 中的 RSS，vRSS 还需要在 Hyper-v 虚拟交换机端口上启用 vRSS \- 。

确定 vRSS 的当前设置，并启用或禁用 VM 的功能。

   **查看当前设置：**

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **已启用此功能：**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>在主机上启用或禁用 vRSS vNIC

确定 vRSS 的当前设置，并为主机 vNIC 启用或禁用该功能。

   **查看当前设置：**

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **启用或禁用此功能：**

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>在 Hyper-v 虚拟交换机端口上配置计划模式
>适用于：Windows Server 2019

在 Windows Server 2019 中，vRSS 可以更新用于动态处理网络流量的逻辑处理器。  具有受支持的驱动程序的设备在默认情况下启用此计划模式。

确定系统上的当前计划模式，或修改 VM 的计划模式。

   **查看当前设置：**

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **设置或修改计划模式：**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>在主机上配置计划模式 vNIC
>适用于：Windows Server 2019

若要确定当前的计划模式或为主机 vNIC 修改计划模式，请使用以下 Windows PowerShell 命令：

   **查看当前设置：**

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **设置或修改计划模式：**

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>相关主题
有关详细信息，请参阅以下参考主题。

- [VMNetworkAdapter](/powershell/module/hyper-v/get-vmnetworkadapter?view=win10-ps)
- [Set-VMNetworkAdapter](/powershell/module/hyper-v/set-vmnetworkadapter?view=win10-ps)

有关详细信息，请参阅[虚拟接收方缩放 (vRSS) ](vrss-top.md)。