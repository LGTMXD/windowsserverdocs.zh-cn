---
title: 边界网关协议 (BGP)
description: 你可以使用本主题了解 Windows Server 2016 中的边界网关协议 (BGP) ，包括 BGP 支持的部署拓扑以及 BGP 特性和功能。
manager: brianlic
ms.topic: article
ms.assetid: 78cc2ce3-a48e-45db-b402-e480b493fab1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8c1b56292c500cdd56c7fe8830ec4ced8bd0b4e8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951432"
---
# <a name="border-gateway-protocol-bgp"></a>边界网关协议 (BGP)

>适用于：Windows Server（半年频道）、Windows Server 2016

可以使用本主题了解边界网关协议 (BGP)，包括 BGP 支持的部署拓扑以及 BGP 特性和功能。

> [!NOTE]
> 除了本主题之外，还提供了以下 BGP 文档。
>
> -   [BGP Windows PowerShell 命令参考](../../remote-access/bgp/BGP-Windows-PowerShell-Command-Reference.md)

本主题包含以下各节：

-   [BGP 支持的部署拓扑](#bkmk_top)

-   [BGP 功能](#bkmk_features)

在多租户模式下，在 Windows Server 2016 远程访问服务 \( RAS \) 网关上配置时，边界网关协议 (BGP) 使你能够管理租户 VM 网络与其远程站点之间的网络流量路由。 你还可以将 BGP 用于单租户 RAS 网关部署，并将远程访问部署为局域网 \( LAN \) 路由器。

BGP 可减少对在路由器上进行手动路由配置的需要，因为它是一种动态路由协议，可自动了解使用站点到站点 VPN 连接进行连接的站点之间的路由。

若要使用 BGP 路由，你必须在计算机或虚拟机 VM 上安装远程访问服务器角色的**远程访问服务 \( RAS \) **和/或**路由**角色服务 \( \) -你使用的系统类型取决于是否具有多租户部署：

-   对于多租户部署，建议在一个或多个 Vm 上安装 RAS 网关。 使用多个 Vm 可提供高可用性。 RAS 网关能够处理来自多个租户的多个连接，由 Hyper-v 主机以及实际配置为网关的 VM 组成。 此网关使用站点到站点 VPN 连接配置为多租户 BGP 路由器，用于交换租户和云服务提供者 \( CSP \) 子网路由。

-   对于单租户边缘网关部署或 LAN 路由器部署，可以在物理计算机或 VM 上安装 RAS 网关。

> [!IMPORTANT]
> 安装 RAS 网关时，必须通过使用**类型**参数值为 "**全部**" 的**enable-remoteaccessroutingdomain** Windows PowerShell 命令来指定是否为每个租户启用 BGP。 若要将远程访问安装为不带多租户功能的启用 BGP 的 LAN 路由器，可以使用命令 " **VpnType RoutingOnly**"。
>
> 下面的示例代码演示了如何在多租户模式下安装 RAS，其中的所有 RAS 功能都 (点到站点 VPN、站点到站点 VPN 和 BGP 路由) 为两个租户（Contoso 和 Fabrikam）启用。

```
$Contoso_RoutingDomain = "ContosoTenant"
$Fabrikam_RoutingDomain = "FabrikamTenant"

Install-RemoteAccess -MultiTenancy

Enable-RemoteAccessRoutingDomain -Name $Contoso_RoutingDomain -Type All -PassThru
Enable-RemoteAccessRoutingDomain -Name $Fabrikam_RoutingDomain -Type All -PassThru
```

## <a name="bgp-supported-deployment-topologies"></a><a name="bkmk_top"></a>BGP 支持的部署拓扑
下面列出了受支持的部署拓扑（其中的企业站点连接到云服务提供程序 (CSP) 数据中心）。

在所有方案中，CSP 网关都是 Windows Server 2016 RAS 网关。 RAS 网关能够处理来自多个租户的多个连接，由 Hyper-v 主机以及实际配置为网关的 VM 组成。 此边缘网关使用站点到站点 VPN 连接配置为多租户 BGP 路由器，用于交换企业和 CSP 子网路由。

租户使用站点到站点 (S2S) VPN 连接来连接到 CSP 数据中心内的资源。 此外，针对企业与 CSP 网关之间的动态路由信息交换部署 BGP 路由协议。

支持以下部署拓扑。

-   [位于企业站点边缘的具有 BGP 的 RAS VPN 站点到站点网关](#bkmk_top1)

-   [处于企业站点边缘的具有 BGP 的第三方网关](#bkmk_top2)

-   [具有第三方网关的多个企业站点](#bkmk_top3)

-   [将不同的终结点用于 BGP 和 VPN](#bkmk_top4)

以下各部分包含有关每个受支持的 BGP 拓扑的其他信息。

### <a name="ras-vpn-site-to-site-gateway-with-bgp-at-enterprise-site-edge"></a><a name="bkmk_top1"></a>位于企业站点边缘的具有 BGP 的 RAS VPN 站点到站点网关
此拓扑描述连接到 CSP 的企业站点。 企业路由拓扑包含一个内部路由器、一个为 VPN 站点到站点连接配置的与 CSP 和一个边缘防火墙设备的 Windows Server 2016 RAS 网关。 RAS 网关会终止 S2S VPN 和 BGP 连接。

![RAS VPN 站点到站点网关](../../media/Border-Gateway-Protocol-BGP/bgp_01.jpg)

两个站点都使用外部边界网关协议 (eBGP) 进行连接，该协议可以在不同自治系统 (AS) 中支持 BGP 的路由器之间传输信息。 这要求企业和 CSP 具有不同的自治系统编号 (ASN)（这是一个参数，是 BGP 协议必不可少的组成部分）。

在此方案中，BGP 的工作方式如下。

-   企业站点边缘设备使用 BGP 了解在云中托管的虚拟化子网路由 (10.2.1.0/24)。 此设备还会将本地子网路由 (10.1.1.0/24) 播发到 CSP RAS 多租户网关。

-   客户边缘路由器通过以下机制之一了解本地内部路由：

    -   边缘设备使用内部路由器运行 BGP 并了解内部路由（在此示例中为 10.1.1.0/24）。 同时，内部路由器了解来自边缘设备的外部路由（如 10.2.1.0/24），内部路由器必须使用内部网关协议 (IGP)（如开放最短路径优先 (OSPF) 或路由信息协议 (RIP)）将这些路由分发到其他本地路由器。

    -   边缘设备可以使用静态路由或接口进行配置，以便使用 BGP选择路由进行播发。 边缘设备还可以使用 IGP 将外部路由分发到其他本地路由器。

### <a name="third-party-gateway-with-bgp-at-enterprise-site-edge"></a><a name="bkmk_top2"></a>处于企业站点边缘的具有 BGP 的第三方网关
此拓扑描绘使用第三方边缘路由器连接到 CSP 的企业站点。 边缘路由器还充当站点到站点 VPN 网关。

![处于企业站点边缘的具有 BGP 的第三方网关](../../media/Border-Gateway-Protocol-BGP/bgp_02.jpg)

企业边缘路由器通过以下机制之一了解本地内部路由：

-   边缘设备使用内部路由器运行 BGP 并了解内部路由（在此示例中为 10.1.1.0/24）。

-   边缘设备实现内部网关协议 (IGP)，并直接参与内部路由。

### <a name="multiple-enterprise-sites-connecting-to-csp-cloud-datacenter"></a><a name="bkmk_top3"></a>连接到 CSP 云数据中心的多个企业站点
此拓扑描绘使用第三方网关连接到 CSP 的多个企业站点。 第三方边缘设备充当站点到站点 VPN 网关和 BGP 路由器。

![连接到 CSP 云数据中心的多个企业站点](../../media/Border-Gateway-Protocol-BGP/bgp_03.jpg)

客户边缘路由器通过以下机制之一了解本地内部路由：

-   边缘设备使用内部路由器运行 BGP 并了解内部路由（在此示例中为 10.1.1.0/24）。

-   边缘设备实现内部网关协议 (IGP)，并直接参与内部路由。

每个企业站点通过直接 eBGP 连接了解来自其他站点的路由。

每个企业站点使用另一个企业站点直接了解承载的网络路由，但不会基于路由的成本选择最佳路由。

如果企业站点1处的 BGP 路由器由于连接失败而无法与 Enterprise Site 2 BGP 路由器连接，则站点 1 BGP 路由器会动态开始从 CSP BGP 路由器了解到 Enterprise Site 2 网络的路由，并且流量通过 CSP 上的 Windows Server BGP 路由器无缝地从站点1重新路由到站点2。

### <a name="separate-termination-points-for-bgp-and-vpn"></a><a name="bkmk_top4"></a>将不同的终结点用于 BGP 和 VPN
此拓扑描绘使用两个不同的路由器作为 BGP 和站点到站点 VPN 终结点的企业。 站点到站点 VPN 在 Windows Server 2016 RAS 网关上终止，而 BGP 在内部路由器上终止。 在连接的 CSP 端，CSP 会终止 VPN 和 BGP 与 RAS 网关之间的连接。 使用此配置时，内部第三方路由器硬件必须支持将 IGP 路由重新分发到 BGP 以及将 BGP 路由重新分发到 IGP。

![将不同的终结点用于 BGP 和 VPN](../../media/Border-Gateway-Protocol-BGP/bgp_04.jpg)

内部路由器通过以下机制之一了解企业路由：

-   BGP

-   内部网关协议 (IGP)，如 OSPF 或 RIP。

-   静态路由配置

在企业站点上使用任何 IGP 时，内部路由器都必须将 IGP 路由重新分发到 BGP 中（以及将 BGP 路由重新分发到 IGP 路由中），以便维持 CSP 虚拟网络与本地企业子网之间的子网连接。

使用此部署时，企业 RAS 网关具有与 CSP RAS 网关之间的站点到站点 VPN 连接，后者向企业 RAS 网关提供到 CSP 网关的路由。 企业内部路由器随后通过将 iBGP 与企业 RAS 网关一起使用来学习与 CSP 网关的路由。 因此，企业内部路由器可以与 CSP RAS 网关 BGP 路由器建立对等互连会话。

今后，企业内部路由器和 CSP RAS 网关会交换路由信息。 企业 RAS BGP 路由器了解 CSP 路由和企业路由，以便以物理方式在网络之间路由数据包。

## <a name="bgp-features"></a><a name="bkmk_features"></a>BGP 功能
以下是 RAS 网关 BGP 路由器的功能。

**作为远程访问的角色服务的 BGP 路由**。 你现在可以安装远程访问服务器角色的**路由**角色服务，而不会在要使用远程访问作为 BGP LAN 路由器的情况下安装**远程访问服务 (RAS) **角色服务。  这会减少 BGP 路由器内存占用量，并且仅安装动态 BGP 路由所需的组件。 当只需要 BGP 路由器 VM 且不需要使用 DirectAccess 或 VPN 时，路由角色服务非常有用。 此外，将远程访问作为带有 BGP 的 LAN 路由器，可提供内部网络上的 BGP 的动态路由优势。

**BGP 统计信息（消息计数器、路由计数器）**。 BGP 路由器支持使用 **Get-BgpStatistics** Windows PowerShell 命令显示消息和路由统计信息（如果需要）。

**相等成本多路径路由 (ECMP) 支持**。 BGP 路由器支持 ECMP，可以将多个相等成本的路由插入到 BGP 路由表和堆栈中。 用于传输数据包的路由的 BGP 路由器在启用了 ECMP 时是随机的。

**HoldTime 配置**。 BGP 路由器支持根据网络要求配置 HoldTimer 值。 此计时器可以动态更改，以适应与第三方设备的互操作性或为 BGP 对等互连会话超时维持特定的最大时间。

**内部 BGP 和外部 BGP 支持**。 BGP 路由器同时支持 iBGP 和 eBGP 对等互连。 若要配置任一 BGP，必须确保将适当的 ASN 分配给本地和远程 BGP 路由器。 所有四种 BGP 部署拓扑都利用 eBGP 对等互连，第四种拓扑还使用 iBGP 对等互连。

**与第三方解决方案的互操作性**。 BGP 路由器基于最新的 BGP 版本 4 规范，经过测试可与大多数主要的第三方 BGP 路由设备进行互操作。 有关详细信息，请参阅征求意见文档 (RFC) 4271 [边界网关协议 4 (BGP-4)](https://tools.ietf.org/html/rfc4271)。

**IPv4 和 IPv6 传输对等互连支持**。 BGP 路由器同时支持 IPv4 和 IPv6 对等互连。 但是，必须将 BGP 标识符配置为 BGP 路由器的 IPv4 地址。 对于所有 BGP 路由器部署拓扑，可以使用两种对等互连类型 (IPV4/IPv6) 中的任一种。

**IPv4 和 IPv6 单播路由学习和播发功能（多协议网络层可访问性信息 [NLRI]）**。 无论使用什么传输，BGP 路由器都可以交换 IPv4 和 IPv6 路由（如果其他 BGP 路由器在建立会话的同时公告相应的功能）。 若要配置 IPv6 路由，必须启用参数 IPv6Routing，并且必须在路由器级别配置本地全局 IPv6 地址。

**混合模式和被动模式对等互连**。 你可以在混合模式（其中 BGP 路由器充当发起方和响应方或被动模式）下配置 BGP 对等会话，其中 BGP 路由器不发起对等互连，但会响应传入的请求。 混合模式是默认模式，建议用于 BGP 对等互连。 除非你要使用被动模式进行调试或诊断，否则情况都是如此。 对于所有 BGP 路由器部署拓扑，混合模式对等互连需要在发生失败事件的情况下实现自动重新启动。

**路由属性重写功能**。 可以使用 BGP 路由策略下一个跃点、MED、Local-Pref 和社区，对 BGP 路由器入口和出口路由播发添加、修改或删除以下属性。

**路由筛选**。 BGP 路由器支持基于多个路由属性（如前缀、ASN 范围、社区和下一个跃点）来筛选入口或出口路由播发。

**路由反射器 (RR) 和 RR 客户端**。 BGP 路由器可以充当路由反射器和 RR 客户端。 这在复杂拓扑中很有用，在这种情况下，RR 可以通过形成 RR 群集来简化网络。

**路由刷新支持**。 BGP 路由器支持路由刷新，并且在默认情况下会在对等互连上播发此功能。 它可以在对等方通过路由刷新消息进行请求时发送一组全新的路由更新，还可以通过发送路由刷新来更新对等节点的路由策略更改等事件中的路由表。 这样就可以在不需要重新启动对等互连的情况下更改或更新 Windows Server 2016 中的 BGP 路由策略。

**静态路由配置支持**。 可以使用 **Add-BgpCustomRoute** Windows PowerShell 命令在 BGP 路由器上配置静态路由或接口。 配置的静态路由可以是必须从中选择路由的接口的前缀或名称。 但是，只有包含可解析的下一个跃点的路由才会插入到 BGP 路由表中并播发给对等方。

**传输路由支持**。 BGP 路由器支持 iBGP 到 iBGP 连接的传输路由、iBGP 到 eBGP 连接以及 eBGP 到 eBGP 连接。

**路由摆动抑制**。 在 Windows Server 2016 中将摆动抑制路由到 BGP 路由支持路由摆动抑制。 例如，当某个路由持续被播发并被提取，使路由表不稳定时，可以将 BGP 路由器配置为向该路由分配一个抑制权重，并为其进行监视，并根据需要对其进行监视。 这有助于维护稳定路由表，并减少 BGP 路由器的处理。

**路由聚合**。 通过将聚合路由到 BGP 路由器，你可以配置聚合路由，并将具有摘要或聚合路由的更细化路由播发替换为对等方。 这会导致在网络上传输的路由播发消息数量越少。

> [!NOTE]
> 在 System Center 中，RAS 网关名为 "Windows Server 网关"。




