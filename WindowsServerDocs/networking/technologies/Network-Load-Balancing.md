---
title: Network Load Balancing
description: 在本主题中，我们将为你提供 \( \) Windows Server 2016 中的网络负载平衡 NLB 功能的概述。 可以使用 NLB 将两个或多个服务器作为单个虚拟群集进行管理。 NLB 增强了 Internet 服务器应用程序（如在 web、FTP、防火墙、代理、虚拟专用网络 \( VPN \) 和其他任务关键服务器上使用的应用程序）的可用性和可伸缩性 \- 。
manager: dougkim
ms.topic: article
ms.assetid: 244a4b48-06e5-4796-8750-a50e4f88ac72
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: ecea87a3716ef68c599594851037e774ad589998
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955804"
---
# <a name="network-load-balancing"></a>Network Load Balancing

>适用于：Windows Server（半年频道）、Windows Server 2016

在本主题中，我们将为你提供 \( \) Windows Server 2016 中的网络负载平衡 NLB 功能的概述。 可以使用 NLB 将两个或多个服务器作为单个虚拟群集进行管理。 NLB 增强了 Internet 服务器应用程序（如在 web、FTP、防火墙、代理、虚拟专用网络 \( VPN \) 和其他任务关键服务器上使用的应用程序）的可用性和可伸缩性 \- 。

> [!NOTE]
> Windows Server 2016 包含一个新的以 Azure 为基础的软件负载均衡器 \( SLB \) ，作为软件定义的网络 \( SDN \) 基础结构的组件。 如果使用的是 SDN，使用非 Windows 工作负荷，需要出站网络地址转换 \( NAT \) ，或者需要第3层 \( \) 或非 TCP 的负载均衡，请使用 SLB 而不是 NLB。 对于非 SDN 部署，可以继续使用 NLB 和 Windows Server 2016。 有关 SLB 的详细信息，请参阅[用于 SDN 的软件负载平衡 (SLB) ](../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)。

网络负载平衡 \( NLB \) 功能使用 TCP IP 网络协议将流量分布到多个服务器上 \/ 。 通过将运行应用程序的两台或多台计算机组合到单个虚拟群集，NLB 可为 web 服务器和其他任务关键型服务器提供可靠性和性能 \- 。

NLB 群集中的服务器称为*主机*，每个主机都运行服务器应用程序的单独副本。 NLB 将传入的客户端请求分发给群集中的各个主机。 可以配置将由每个主机处理的负载。 还可以动态地向群集中添加主机，以处理增长的负载。 NLB 还可以将所有流量引导至指定的单个主机，该主机称为*默认主机*。

NLB 允许使用同一组 IP 地址指定群集中所有计算机的地址，而且它还为每个主机保留一组唯一且专用的 IP 地址。 对于负载 \- 平衡的应用程序，当主机出现故障或脱机时，会自动在仍在运行的计算机之间重新分配负载。 准备就绪时，可以将脱机计算机以透明方式重新加入群集，并重新获取其工作量共享，以便使群集中的其他计算机处理更少的流量。

## <a name="practical-applications"></a>实际的应用程序
NLB 有助于确保无状态应用程序（例如运行 Internet Information Services IIS 的 web 服务器 \( \) ）在最短的停机时间内可用，并可 \( 通过在负载增加时添加更多服务器来进行缩放 \) 。 以下部分描述了 NLB 如何支持运行这些应用程序的群集服务器的高可用性、可伸缩性和可管理性。

### <a name="high-availability"></a>高可用性
通过最大程度地减少停机时间，高可用性系统能够可靠地提供可接受级别的服务。 为了提供高可用性，NLB 包含内置 \- 功能，可自动执行以下操作：

-   检测群集主机是否发生故障或脱机，然后进行恢复。

-   在添加或删除主机时平衡网络负载。

-   在十秒之内恢复并重新分发负载。

### <a name="scalability"></a>可伸缩性
可伸缩性是度量计算机、服务或应用程序如何更好地改进以满足持续增长的性能需求的标准。 对于 NLB 群集而言，可伸缩性是指当群集的全部负载超过其能力时逐步将一个或多个系统添加到现有群集中的功能。 为支持可伸缩性，可通过 NLB 执行以下操作：

-   平衡 NLB 群集上单个 TCP IP 服务的负载请求 \/ 。

-   在一个群集中最多支持 32 台计算机。

-   在 \( \) 群集中的多个主机之间平衡来自同一客户端或多个客户端的多个服务器加载请求。

-   随着负载的增加，将主机添加到 NLB 群集，这样不会导致群集发生故障。

-   在负载降低时从群集中删除主机。

-   通过全部实现管道化提高性能并降低开销。 管道允许向 NLB 群集发送请求，而无需等待响应上一个请求。

### <a name="manageability"></a>可管理性
为支持可管理性，可通过 NLB 执行以下操作：

-   使用 NLB 管理器或[Windows PowerShell 中的网络负载平衡 (nlb) cmdlet](https://technet.microsoft.com/library/hh801274.aspx)来管理和配置多个 nlb 群集和群集主机。

-   使用端口管理规则，可以为单个 IP 端口或端口组指定负载平衡行为。

-   为每个网站定义不同的端口规则。 如果 \- 对多个应用程序或网站使用相同的一组负载平衡服务器，则端口规则基于目标虚拟 IP 地址（ \( 使用虚拟群集） \) 。

-   使用可选的单主机规则，将所有客户端请求定向到单个主机 \- 。 NLB 将客户端请求路由到运行特定应用程序的特定主机。

-   阻止对某些 IP 端口进行不需要的网络访问。

-   启用 \( 群集主机上的 Internet 组管理协议 IGMP \) 支持，控制交换机端口流 \( ，其中传入的网络数据包将在 \) 多播模式下运行时发送到交换机上的所有端口。

-   通过使用 Windows PowerShell 命令或脚本，远程启动、停止和控制 NLB 操作。

-   查看 Windows 事件日志以检查 NLB 事件。 NLB 在事件日志中记录所有操作和群集更改。

## <a name="important-functionality"></a>重要功能

NLB 作为标准的 Windows Server 网络驱动程序组件进行安装。 它的操作对于 TCP \/ IP 网络堆栈是透明的。 下图显示了在典型配置中 NLB 和其他软件组件之间的关系。

![网络负载平衡和其他软件组件](../media/NLB/nlb.jpg)

下面是 NLB 的主要功能。

- 不需要更改任何硬件即可运行。

- 提供网络负载平衡工具，以从单个远程或本地计算机配置和管理多个群集和所有主机。

- 允许客户端使用单个逻辑 Internet 名称和虚拟 IP 地址（称为群集 IP 地址）来访问群集， \( 它会保留每台计算机的各个名称 \) 。 NLB 允许多宿主服务器具有多个虚拟 IP 地址。

> [!NOTE]
> 将 Vm 作为虚拟群集部署时，NLB 不要求服务器是多宿主的，才能具有多个虚拟 IP 地址。

- 可以将 NLB 绑定到多个网适配器，这样你便可以在每个主机上配置多个独立的群集。 支持多个网络适配器与虚拟群集不同，因为虚拟群集允许你在单个网络适配器上配置多个群集。

- 无需对服务器应用程序进行修改，这样它们可以在 NLB 群集中运行。

- 如果群集主机发生故障并随后联机重新提交，可以配置为自动添加主机到群集。 添加的主机将能够开始处理来自客户端的新的服务器请求。

-   可以在不打扰其他主机上群集操作的情况下使计算机脱机进行预防性的维护。

## <a name="hardware-requirements"></a>硬件要求
下面是运行 NLB 群集的硬件要求。

-   群集中的所有主机必须驻留于同一子网中。

-   每台主机上网络适配器的数量不受限制，不同的主机可以有不同数量的适配器。

-   在每个群集中，所有网络适配器都必须为全为多播或者全为单播。 NLB 不支持在单个群集中同时启用多播和单播。

-   如果使用单播模式，用于处理客户端 \- 到群集通信的网络适配器 \- 必须支持更改其媒体访问控制 \( MAC \) 地址。

## <a name="software-requirements"></a>软件要求
下面是运行 NLB 群集的软件要求。

-   在 \/ 每个主机上启用 NLB 的适配器上只能使用 TCP IP。 不要添加任何其他协议 \( ，例如 IPX \) 到此适配器。

-   该群集中服务器的 IP 地址必须为静态地址。

> [!NOTE]
> NLB 不支持动态主机配置协议 \( DHCP \) 。 NLB 在其配置的每个接口上禁用 DHCP。

## <a name="installation-information"></a>安装信息
你可以使用服务器管理器或用于 NLB 的 Windows PowerShell 命令来安装 NLB。

或者，还可以安装网络负载平衡工具来管理本地或远程 NLB 群集。 这些工具包括网络负载平衡管理器和 NLB Windows PowerShell 命令。

### <a name="installation-with-server-manager"></a>安装服务器管理器

在服务器管理器中，你可以使用 "添加角色和功能向导" 来添加**网络负载平衡**功能。 完成向导后，会安装 NLB，无需重新启动计算机。


### <a name="installation-with-windows-powershell"></a>安装 Windows PowerShell

若要使用 Windows PowerShell 安装 NLB，请在要安装 NLB 的计算机上提升了权限的 Windows PowerShell 提示符处运行以下命令。

```powershell
Install-WindowsFeature NLB -IncludeManagementTools
```

安装完成后，不需要重新启动计算机。

有关详细信息，请参阅[Install](https://docs.microsoft.com/powershell/module/servermanager/install-windowsfeature?view=win10-ps)。

### <a name="network-load-balancing-manager"></a>网络负载平衡管理器
若要在服务器管理器中打开网络负载平衡管理器，请单击“工具”****，然后单击“网络负载平衡管理器”****。

## <a name="additional-resources"></a>其他资源
下表提供了指向有关 NLB 功能的其他信息的链接。

|内容类型|参考|
|----------------|--------------|
|部署|[网络负载平衡部署指南](https://technet.microsoft.com/library/cc754833(WS.10).aspx)&#124;[用终端服务配置网络负载平衡](https://technet.microsoft.com/library/cc771300(v=WS.10).aspx)|
|操作|[管理网络负载平衡群集](https://technet.microsoft.com/library/cc753954(WS.10).aspx)&#124;[设置网络负载平衡参数](https://technet.microsoft.com/library/cc731619(WS.10).aspx)&#124;[控制网络负载平衡群集上的主机](https://technet.microsoft.com/library/cc770870(WS.10).aspx)|
|疑难解答|[排查网络负载平衡群集](https://technet.microsoft.com/library/cc732592(WS.10).aspx)&#124; [NLB 群集事件和错误](https://technet.microsoft.com/library/cc731678(WS.10).aspx)|
|工具和设置|[网络负载平衡 Windows PowerShell cmdlet](https://go.microsoft.com/fwlink/p/?LinkId=238123)|
|社区资源|[高可用性 \( 群集 \) 论坛](https://go.microsoft.com/fwlink/p/?LinkId=230641)
