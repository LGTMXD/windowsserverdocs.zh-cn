---
title: 配置 RADIUS 通信防火墙
description: 本主题概述了如何配置防火墙以允许 Windows Server 2016 中的网络策略服务器的 RADIUS 流量。
manager: brianlic
ms.topic: article
ms.assetid: 58cca2b2-4ef3-4a09-a614-8bdc08d24f15
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ac1ec981b83607643d295411648c6f38892490f3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937398"
---
# <a name="configure-firewalls-for-radius-traffic"></a>配置 RADIUS 通信防火墙

>适用于：Windows Server（半年频道）、Windows Server 2016

可以将防火墙配置为允许或阻止各种类型的 IP 通信来回于运行防火墙的计算机或设备。 如果未将防火墙正确配置为允许在 RADIUS 客户端、RADIUS 代理和 RADIUS 服务器中进行 RADIUS 通信，则网络访问身份验证可能会失败，从而阻止用户访问网络资源。

你可能需要配置两种类型的防火墙以允许 RADIUS 流量：

- 运行网络策略服务器的本地服务器上具有高级安全性的 Windows Defender 防火墙)  (NPS。
- 运行于其他计算机或硬件设备的防火墙。

## <a name="windows-firewall-on-the-local-nps"></a>本地 NPS 上的 Windows 防火墙

默认情况下，NPS 通过使用用户数据报协议 \( UDP \) 端口1812、1813、1645和1646来发送和接收 RADIUS 流量。 NPS 上的 Windows Defender 防火墙会自动配置为在安装 NPS 期间出现异常，以允许发送和接收此 RADIUS 流量。

因此，如果您使用的是默认 UDP 端口，则不需要更改 Windows Defender 防火墙配置，以允许与 NPSs 之间的 RADIUS 通信。

在某些情况下，您可能需要更改 NPS 用于 RADIUS 通信的端口。 如果将 NPS 和网络访问服务器配置为在默认端口以外的端口上发送和接收 RADIUS 通信，则必须执行以下操作：

- 删除允许默认端口上的 RADIUS 流量的例外。
- 创建新的例外，以允许新端口上的 RADIUS 流量。

有关详细信息，请参阅[配置 NPS UDP 端口信息](nps-udp-ports-configure.md)。

## <a name="other-firewalls"></a>其他防火墙

在最常见的配置中，防火墙连接到 Internet，NPS 是连接到外围网络的 intranet 资源。

若要访问 intranet 内的域控制器，NPS 可能会执行以下操作：

- 在外围网络和 Intranet（未启用 IP 路由）上分别有一个接口。
- 在外围网络上有一个单一接口。 在此配置中，NPS 通过将外围网络连接到 intranet 的另一防火墙与域控制器通信。

## <a name="configuring-the-internet-firewall"></a>配置 Internet 防火墙

连接到 Internet 的防火墙必须在其 Internet 接口上配置输入和输出筛选器， \( 并且可以选择其网络外围接口， \) 以允许在 NPS 和 RADIUS 客户端或 Internet 上的代理之间转发 RADIUS 消息。 可以使用其他筛选器来允许将通信传递到外围网络上的 Web 服务器、VPN 服务器和其他类型的服务器。

可以在 Internet 接口和外围网络接口上配置单独的输入和输出数据包筛选器。

### <a name="configure-input-filters-on-the-internet-interface"></a>在 Internet 接口上配置输入筛选器

在防火墙的 Internet 接口上配置以下输入数据包筛选器，以允许以下类型的通信：

- 外围网络接口的目标 IP 地址和 UDP 目标端口 1812 (0x714) NPS。  此筛选器允许从基于 Internet 的 RADIUS 客户端到 NPS 的 RADIUS 身份验证通信。 这是 NPS 使用的默认 UDP 端口，如 RFC 2865 中所定义。 如果使用其他端口，请将该端口号替换为1812。
- 外围网络接口的目标 IP 地址和 UDP 目标端口 1813 (0x715) NPS。 此筛选器允许从基于 Internet 的 RADIUS 客户端到 NPS 的 RADIUS 记帐通信。 这是 NPS 使用的默认 UDP 端口，如 RFC 2866 中所定义。 如果使用其他端口，请将该端口号替换为1813。
- \(\)外围网络接口的可选目标 IP 地址和 NPS 的 1645 0x66D 的 UDP 目标端口 \( \) 。 此筛选器允许从基于 Internet 的 RADIUS 客户端到 NPS 的 RADIUS 身份验证通信。 这是旧 RADIUS 客户端使用的 UDP 端口。
- \(\)外围网络接口的可选目标 IP 地址和 NPS 的 1646 0x66E 的 UDP 目标端口 \( \) 。 此筛选器允许从基于 Internet 的 RADIUS 客户端到 NPS 的 RADIUS 记帐通信。 这是旧 RADIUS 客户端使用的 UDP 端口。

### <a name="configure-output-filters-on-the-internet-interface"></a>在 Internet 接口上配置输出筛选器

在防火墙的 Internet 接口上配置以下输出筛选器，以允许以下类型的通信：

- 外围网络接口的源 IP 地址和 UDP 源端口 1812 (0x714) NPS。 此筛选器允许从 NPS 到基于 Internet 的 RADIUS 客户端的 RADIUS 身份验证流量。 这是 NPS 使用的默认 UDP 端口，如 RFC 2865 中所定义。 如果使用其他端口，请将该端口号替换为1812。
- 外围网络接口的源 IP 地址和 UDP 源端口 1813 (0x715) NPS。 此筛选器允许从 NPS 到基于 Internet 的 RADIUS 客户端的 RADIUS 记帐通信。 这是 NPS 使用的默认 UDP 端口，如 RFC 2866 中所定义。 如果使用其他端口，请将该端口号替换为1813。
- \(\)外围网络接口的可选源 IP 地址和 NPS 的 1645 0x66D 的 UDP 源端口 \( \) 。 此筛选器允许从 NPS 到基于 Internet 的 RADIUS 客户端的 RADIUS 身份验证流量。 这是旧 RADIUS 客户端使用的 UDP 端口。
- \(\)外围网络接口的可选源 IP 地址和 NPS 的 1646 0x66E 的 UDP 源端口 \( \) 。 此筛选器允许从 NPS 到基于 Internet 的 RADIUS 客户端的 RADIUS 记帐通信。 这是旧 RADIUS 客户端使用的 UDP 端口。

### <a name="configure-input-filters-on-the-perimeter-network-interface"></a>在外围网络接口上配置输入筛选器

在防火墙的外围网络接口上配置以下输入筛选器，以允许以下类型的通信：

- 外围网络接口的源 IP 地址和 UDP 源端口 1812 (0x714) NPS。 此筛选器允许从 NPS 到基于 Internet 的 RADIUS 客户端的 RADIUS 身份验证流量。 这是 NPS 使用的默认 UDP 端口，如 RFC 2865 中所定义。 如果使用其他端口，请将该端口号替换为1812。
- 外围网络接口的源 IP 地址和 UDP 源端口 1813 (0x715) NPS。 此筛选器允许从 NPS 到基于 Internet 的 RADIUS 客户端的 RADIUS 记帐通信。 这是 NPS 使用的默认 UDP 端口，如 RFC 2866 中所定义。 如果使用其他端口，请将该端口号替换为1813。
- \(\)外围网络接口的可选源 IP 地址和 NPS 的 1645 0x66D 的 UDP 源端口 \( \) 。 此筛选器允许从 NPS 到基于 Internet 的 RADIUS 客户端的 RADIUS 身份验证流量。 这是旧 RADIUS 客户端使用的 UDP 端口。
- \(\)外围网络接口的可选源 IP 地址和 NPS 的 1646 0x66E 的 UDP 源端口 \( \) 。 此筛选器允许从 NPS 到基于 Internet 的 RADIUS 客户端的 RADIUS 记帐通信。 这是旧 RADIUS 客户端使用的 UDP 端口。

### <a name="configure-output-filters-on-the-perimeter-network-interface"></a>在外围网络接口上配置输出筛选器

在防火墙的外围网络接口上配置以下输出数据包筛选器，以允许以下类型的通信：

- 外围网络接口的目标 IP 地址和 UDP 目标端口 1812 (0x714) NPS。 此筛选器允许从基于 Internet 的 RADIUS 客户端到 NPS 的 RADIUS 身份验证通信。 这是 NPS 使用的默认 UDP 端口，如 RFC 2865 中所定义。 如果使用其他端口，请将该端口号替换为1812。
- 外围网络接口的目标 IP 地址和 UDP 目标端口 1813 (0x715) NPS。 此筛选器允许从基于 Internet 的 RADIUS 客户端到 NPS 的 RADIUS 记帐通信。 这是 NPS 使用的默认 UDP 端口，如 RFC 2866 中所定义。 如果使用其他端口，请将该端口号替换为1813。
- \(\)外围网络接口的可选目标 IP 地址和 NPS 的 1645 0x66D 的 UDP 目标端口 \( \) 。 此筛选器允许从基于 Internet 的 RADIUS 客户端到 NPS 的 RADIUS 身份验证通信。 这是旧 RADIUS 客户端使用的 UDP 端口。
- \(\)外围网络接口的可选目标 IP 地址和 NPS 的 1646 0x66E 的 UDP 目标端口 \( \) 。 此筛选器允许从基于 Internet 的 RADIUS 客户端到 NPS 的 RADIUS 记帐通信。 这是旧 RADIUS 客户端使用的 UDP 端口。

为了增加安全性，你可以使用每个 RADIUS 客户端的 IP 地址，该客户端通过防火墙发送数据包，为外围网络上的客户端与 NPS 的 IP 地址之间的流量定义筛选器。

### <a name="filters-on-the-perimeter-network-interface"></a>外围网络接口上的筛选器

在 Intranet 防火墙的外围网络接口上配置以下输入数据包筛选器，以允许以下类型的通信：

- NPS 外围网络接口的源 IP 地址。 此筛选器允许来自外围网络上 NPS 的流量。

在 Intranet 防火墙的外围网络接口上配置以下输出筛选器，以允许以下类型的通信：

- NPS 外围网络接口的目标 IP 地址。 此筛选器允许流量发送到外围网络上的 NPS。

### <a name="filters-on-the-intranet-interface"></a>Intranet 接口上的筛选器

在防火墙的 Intranet 接口上配置以下输入筛选器，以允许以下类型的通信：

- NPS 外围网络接口的目标 IP 地址。 此筛选器允许流量发送到外围网络上的 NPS。

在防火墙的 Intranet 接口上配置以下输出数据包筛选器，以允许以下类型的通信：

- NPS 外围网络接口的源 IP 地址。 此筛选器允许来自外围网络上 NPS 的流量。


有关管理 NPS 的详细信息，请参阅[管理网络策略服务器](nps-manage-top.md)。

有关 NPS 的详细信息，请参阅[网络策略服务器 (nps) ](nps-top.md)。




