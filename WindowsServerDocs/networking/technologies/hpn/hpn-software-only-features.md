---
title: 仅软件 (SO) 功能和技术
description: 这些功能实现为操作系统的一部分，并且独立于基础 NIC (的) 。 有时，这些功能需要对 NIC 进行某种优化才能实现最佳操作。 其中的示例包括 Hyper-v 功能，如虚拟机服务质量 (vmQoS) 、访问控制列表 (Acl) 和非 Hyper-v 功能，如 NIC 组合。
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: 94b7a4b87a74c24acc97289516f6835be9b90ef7
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990312"
---
# <a name="software-only-so-features-and-technologies"></a>仅软件 (SO) 功能和技术
仅软件功能作为操作系统的一部分实现，并且独立于基础 NIC () 。 有时，这些功能需要对 NIC 进行某种优化才能实现最佳操作。 其中的示例包括 Hyper-v 功能，如虚拟机服务质量 (vmQoS) 、访问控制列表 (Acl) 和非 Hyper-v 功能，如 NIC 组合。

## <a name="access-control-lists-acls"></a>访问控制列表 (ACL)

用于管理 VM 安全性的 Hyper-v 和 SDNv1 功能。 此功能适用于非虚拟化的 Hyper-v 堆栈和 HVNv1 堆栈。 可以通过[get-vmnetworkadapteracl](/powershell/module/hyper-v/add-vmnetworkadapteracl?view=win10-ps)和[get-vmnetworkadapteracl](/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell Cmdlet 管理 hyper-v 交换机 acl。

## <a name="extended-acls"></a>扩展的 Acl

使用 hyper-v 虚拟交换机扩展 Acl，你可以配置 Hyper-v 虚拟交换机扩展端口 Acl，为数据中心的租户 Vm 提供防火墙保护和强制实施安全策略。 由于端口 Acl 是在 Hyper-v 虚拟交换机上配置的，而不是在 Vm 内配置的，因此管理员可以管理多租户环境中所有租户的安全策略。

可以通过[add-vmnetworkadapterextendedacl](/powershell/module/hyper-v/add-vmnetworkadapterextendedacl?view=win10-ps)和[add-vmnetworkadapterextendedacl](/powershell/module/hyper-v/remove-vmnetworkadapteracl?view=win10-ps) PowerShell cmdlet 管理 hyper-v 交换机扩展 acl。

>[!TIP]
>此功能适用于 HNVv1 堆栈。 对于 SDN 堆栈中的 Acl，请参阅下面的软件定义的网络 SDN) Acl。

有关此库中的扩展端口访问控制列表的详细信息，请参阅[使用扩展端口访问控制列表创建安全策略](../../../virtualization/hyper-v-virtual-switch/create-security-policies-with-extended-port-access-control-lists.md)。

## <a name="nic-teaming"></a>NIC 组合

NIC 组合（也称为 NIC 捆绑）是将多个 NIC 端口聚合到一个实体中的主机，该主机将其视为单个 NIC 端口。 NIC 组合可防止单个 NIC 端口 (或连接到它) 的电缆发生故障。 它还聚合网络流量以提高吞吐量。 有关更多详细信息，请参阅[NIC 组合](../nic-teaming/nic-teaming.md)。

对于 Windows Server 2016，你可以通过两种方式进行组合：

1.  Windows Server 2012 组合解决方案

2.  Windows Server 2016 交换机嵌入组合 (集) 


## <a name="rsc-in-the-vswitch"></a>VSwitch 中的 RSC

在 vSwitch 中 (RSC) 的接收段合并功能是一种功能，该功能采用属于相同流的数据包并到达网络中断之间，并将它们合并为单个数据包，然后将它们传递给操作系统。 Windows Server 2019 中的虚拟交换机具有此功能。 有关此功能的更多详细信息，请参阅[vSwitch 中的接收段合并](./rsc-in-the-vswitch.md)。

## <a name="software-defined-networking-sdn-acls"></a>软件定义的网络 (SDN) Acl

Windows Server 2016 中的 SDN 扩展改进了支持 Acl 的方式。 在 Windows Server 2016 SDN v2 堆栈中，使用了 SDN Acl，而不是 Acl 和扩展 Acl。 可以使用网络控制器来管理 SDN Acl。

## <a name="sdn-quality-of-service-qos"></a>SDN 服务质量 (QoS)

Windows Server 2016 中的 SDN 扩展提供了在5元组的基础上 (出口保留、出口限制和入口限制) 提供带宽控制的方式。 通常，这些策略适用于 vNIC 或 vmNIC 级别，但你可以将它们设置得更加具体。 在 Windows Server 2016 SDN v2 堆栈中，使用了 SDN QoS，而不是 vmQoS。 可以使用网络控制器来管理 SDN QoS。

## <a name="switch-embedded-teaming-set"></a>切换嵌入组合 (集) 

SET 是一种备用 NIC 组合解决方案，可用于在 Windows Server 2016 中包含 Hyper-v 的环境和软件定义的网络 (SDN) 堆栈。 将一些 NIC 组合功能集成到 Hyper-v 虚拟交换机。 有关此库中的交换机嵌入组合的信息，请参阅[ (RDMA 的远程直接内存访问) 和交换机嵌入组合 (设置) ](../../../virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md)。

## <a name="virtual-receive-side-scaling-vrss"></a>虚拟接收方缩放 (vRSS)

软件 vRSS 用于将目标为 VM 的传入流量分散到 VM (LPs) 的多个逻辑处理器。 软件 vRSS 允许 VM 处理的网络流量比单个 LP 能够处理的网络流量多。 有关详细信息，请参阅[虚拟接收方缩放 (vRSS) ](../vrss/vrss-top.md)。

## <a name="virtual-machine-quality-of-service-vmqos"></a>虚拟机服务质量 (vmQoS) 

虚拟机服务质量是一项 Hyper-v 功能，它允许交换机对每个 VM 生成的流量设置限制。 它还允许 VM 在外部网络连接上保留一个带宽量，以便一个 VM 无法枯竭其他 VM 的带宽。 在 Windows Server 2016 SDN v2 堆栈中，SDN QoS 将替换 vmQoS。

vmQoS 可以设置出口限制和出口预留。 创建 Hyper-v 交换机之前，必须确定出口保留模式 (相对权重或绝对带宽) 。

-  确定包含新的 VMSwitch PowerShell cmdlet 的– MinimumBandwidthMode 参数的出口预留模式。

-  将出口限制的值设置为 VMNetworkAdapter PowerShell cmdlet 上的– MaximumBandwidth 参数。

-  将出口预订的值设置为 Set VMNetworkAdapter PowerShell cmdlet 的以下任一参数：

   -  如果新的 VMSwitch cmdlet 上的– MinimumBandwidthMode 参数是绝对参数，请在 Set VMNetworkAdapter cmdlet 上设置– MinimumBandwidthAbsolute 参数。

   -  如果新的 VMSwitch cmdlet 上的– MinimumBandwidthMode 参数是权重，则在 Set VMNetworkAdapter cmdlet 上设置– MinimumBandwidthWeight 参数。

由于此功能使用的算法存在限制，因此建议最大权重或绝对带宽不能超过最低权重或绝对带宽的20倍。 如果需要更多控制，请考虑使用 SDN 堆栈和 SDN QoS 功能。


---