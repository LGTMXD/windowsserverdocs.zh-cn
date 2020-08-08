---
title: Hyper-V 虚拟交换机
description: 本主题概述了 Windows Server 2016 中的 Hyper-v 虚拟交换机。
manager: brianlic
ms.topic: article
ms.assetid: 398440ac-5988-41ce-b91e-eab343a255d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1e2db53f28ff5262778b36b8a5cb91e6062ca9c0
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995703"
---
# <a name="hyper-v-virtual-switch"></a>Hyper-V 虚拟交换机

>适用于：Windows Server（半年频道）、Windows Server 2016

本主题概述了 Hyper-v 虚拟交换机，使你能够将虚拟机 \( vm 连接 \) 到 hyper-v 主机外部的网络 \- ，包括你的组织的 intranet 和 Internet。

\-部署软件定义的网络 SDN 时，还可以连接到运行 hyper-v 的服务器上的虚拟网络 \( \) 。

> [!NOTE]
> 除了本主题，以下 Hyper-v 虚拟交换机文档也可用。
>
> - [管理 Hyper-V 虚拟交换机](Manage-Hyper-V-Virtual-Switch.md)
> - [远程直接内存访问 (RDMA) 和交换机嵌入式组合 (SET)](RDMA-and-Switch-Embedded-Teaming.md)
> - [Windows PowerShell 中的网络交换机组 Cmdlet](/powershell/module/netswitchteam/new-netswitchteam?view=win10-ps)
> - [VMM 2016 中的新增功能](/system-center/vmm/whats-new#networking)
> - [设置 VMM 网络构造](/system-center/vmm/manage-networks)
> - [Hyper-V 论坛](/answers/topics/windows-server-hyper-v.html)
> - [Hyper-V：如果第三方扩展需要，应启用 WFP 虚拟交换机扩展](/answers/topics/windows-server-hyper-v.html)
>
> 有关其他网络技术的详细信息，请参阅[Windows Server 2016 中的网络](../../networking/index.yml)。

Hyper-v \- 虚拟交换机是基于软件的第2层以太网网络交换机， \- 当你安装 hyper-v 服务器角色时，它可在 Hyper-v 管理器中找到 \- 。

Hyper-v 虚拟交换机包含以编程方式管理的功能，可将 Vm 连接到虚拟网络和物理网络。 此外，Hyper-V 虚拟交换机提供了安全、隔离和服务级别的策略执行。

> [!NOTE]
> HYPER-V 虚拟交换机仅支持以太网，不支持其他任何有线局域网 (LAN) 技术（如 Infiniband 和光纤通道）。

Hyper-v 虚拟交换机包括租户隔离功能、流量整形、针对恶意虚拟机的保护，以及简化的故障排除。

利用内置的网络设备接口规范 \( NDIS \) 筛选器驱动程序和 Windows 筛选平台 \( WFP \) 标注驱动程序支持，hyper-v 虚拟交换机使独立软件供应商 \( isv 可以 \) 创建可扩展的插件（称为虚拟交换机扩展）以提供增强的网络和安全功能。 你添加到 Hyper-V 虚拟交换机的虚拟交换机扩展列在 Hyper-V 管理器的虚拟交换机管理器功能中。

在下图中，VM 具有通过交换机端口连接到 Hyper-v 虚拟交换机的虚拟 NIC。

![虚拟交换机连接](../media/Hyper-V-Virtual-Switch/Vswitch_01.jpg)

Hyper-v 虚拟交换机功能为你提供了更多选项，可用于强制实施租户隔离、整形和控制网络流量，并为恶意 Vm 提供保护措施。

>[!NOTE]
> 在 Windows Server 2016 中，具有虚拟 NIC 的 VM 精确显示虚拟 NIC 的最大吞吐量。 若要在 "**网络连接**" 中查看虚拟 nic 速度，请右键单击所需的虚拟 nic 图标，然后单击 "**状态**"。 此时将打开 "虚拟 NIC**状态**" 对话框。 在 "**连接**" 中，"**速度**" 与服务器中安装的物理 NIC 的速度相匹配。

## <a name="uses-for-hyper-v-virtual-switch"></a><a name="bkmk_apps"></a>用于 Hyper-v 虚拟交换机

下面是 Hyper-v 虚拟交换机的一些用例方案。

**显示统计信息**：托管云供应商的开发人员实现了显示 hyper-v 虚拟交换机当前状态的管理包。 该管理程序包可以使用 WMI 来查询交换机范围的当前能力、配置设置和单个端口网络统计。 然后会显示交换机的状态，为管理员提供交换机状态的快速视图。

**资源跟踪**：托管公司根据成员级别销售托管服务。 各种成员级别包括不同的网络性能级别。 管理员以平衡网络可用性的方式分配资源，以符合服务级别协议 (SLA)。 管理员以编程方式跟踪所分配的带宽的当前使用情况，以及虚拟机 (VM) 分配的虚拟机队列 (VMQ) 或 "下通道" 的虚拟机数。 除了为了进行复式记帐追踪或资源而分配的 VM 资源，同一个程序还周期性地记录使用中的资源。

**管理交换机扩展的顺序**：企业已在其 hyper-v 主机上安装了扩展，用于监视流量和报告入侵检测。 在维护时，某些扩展可能被更新了，导致扩展的顺序变更。 运行了一个简单的脚本程序来记录更新后的扩展。

**转发扩展管理 VLAN ID**：一个主要交换机公司正在建立应用所有网络策略的转发扩展。 受管理的一个元素是虚拟局域网 (VLAN) ID。 虚拟交换机将 VLAN 的控制移交给转发扩展。 交换机公司的安装以编程方式调用 Windows Management Instrumentation (WMI) 应用程序编程接口 (API) ，这会打开透明，通知 Hyper-v 虚拟交换机通过 VLAN 标记，无需执行任何操作。

## <a name="hyper-v-virtual-switch-functionality"></a><a name="bkmk_func"></a>Hyper-v 虚拟交换机功能

Hyper-V 虚拟交换机包含的主要功能包括：

-   **Arp/ND 中毒 (欺骗) 保护**：针对使用地址解析协议的恶意 VM 提供防护， (ARP) 欺骗来窃取其他 VM 的 IP 地址。 针对使用邻居发现 (ND) 欺诈的 IPv6 进行的攻击提供防护。

-   **DHCP 保护保护**：可防止将自身表示为动态主机配置协议的恶意 VM (用于中间人攻击的 DHCP) 服务器。

-   **端口 acl**：提供基于媒体访问控制的流量筛选 (MAC) 或 Internet 协议 (IP) 地址/范围，使你能够设置虚拟网络隔离。

-   **VM 的干线模式**：使管理员可以将特定的 VM 设置为虚拟设备，然后将来自各种 vlan 的流量定向到该 vm。

-   **网络流量监视**：使管理员可以查看遍历网络交换机的流量。

-   **隔离 (专用) VLAN**：使管理员可以将流量隔离在多个 vlan 上，以便更轻松地建立隔离的租户社区。

以下是能够增强 Hyper-V 虚拟交换机可用性的一系列功能：

-   **带宽限制和突发支持**：带宽的最小值保证预留的带宽量。 最大带宽超过一个 VM 能够消耗的带宽。

-   **显式拥塞通知 (ECN) 标记支持**： ECN 标记（也称为 Data 中心 TCP (DCTCP) ）使物理交换机和操作系统能够控制流量流，以便交换机的缓冲资源不会溢出，从而增加流量吞吐量。

-   **诊断**：通过诊断，可以通过虚拟交换机轻松跟踪和监视事件和数据包。