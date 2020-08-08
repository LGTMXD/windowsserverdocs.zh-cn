---
title: 步骤2规划 DirectAccess 部署
description: 本主题是有关 Windows Server 2016 的将 DirectAccess 添加到现有远程访问 (VPN) 部署的指南的一部分
manager: brianlic
ms.topic: article
ms.assetid: 72b5b2af-6925-41e0-a3f9-b8809ed711d1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8a31dc9362e9165ae2385de62f8146b769fc8563
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969234"
---
# <a name="step-2-plan-the-directaccess-deployment"></a>步骤2规划 DirectAccess 部署

>适用于：Windows Server（半年频道）、Windows Server 2016

在规划远程访问基础结构之后，启用 DirectAccess 的下一步是规划启用 DirectAccesss 向导的设置。

|任务|描述|
|----|--------|
|规划客户端部署|规划如何使客户端计算机可以使用 DirectAccess 进行连接。 确定将配置为 DirectAccess 客户端的托管服务器。|
|规划远程访问服务器部署|规划如何部署远程访问服务器。|

## <a name="planning-for-client-deployment"></a><a name="bkmk_2_1_client"></a>规划客户端部署
在规划客户端部署时，要作出两个决策：

-   DirectAccess 仅对移动计算机可用，还是对任何一台计算机都可用？

    在启用 DirectAccess 向导中配置 DirectAccess 客户端时，你可以选择仅允许指定的安全组中的移动计算机使用 DirectAccess 进行连接。 如果你限制了移动计算机的访问权限，则远程访问将自动配置 WMI 筛选器以确保 DirectAccess 客户端 GPO 仅应用于指定安全组中的移动计算机。 远程访问管理员需要创建或修改组策略 WMI 筛选器的权限，以启用此设置。

-   哪些安全组将包含 DirectAccess 客户端计算机？

    DirectAccess 设置包含在 DirectAccess 客户端 GPO 中。 GPO 应用于作为安全组一部分的计算机，你在启用 DirectAccess 向导中指定了这些安全组。 你可以指定受支持的任何域中包含的安全组。 在配置远程访问之前，应创建安全组。 你可以在完成远程访问部署后将计算机添加到安全组，但请注意，如果你要将位于不同域的客户端计算机添加到安全组，则客户端 GPO 将不会应用于这些客户端。 例如，如果在域 A 中为 DirectAccess 客户端创建 SG1，之后将客户端从域 B 添加到该组，则客户端 GPO 不会应用于域 B 中的客户端。若要避免此问题，请为每个包含客户端计算机的域创建一个新的客户端安全组。 另外，如果你不希望创建一个新的安全组，则可使用新域的新 GPO 名称运行 Add-DAClient cmdlet。

## <a name="planning-for-remote-access-server-deployment"></a><a name="bkmk_2_2_server"></a>规划远程访问服务器部署
在规划部署远程访问服务器时，需要作出许多决策：

-   **网络拓扑**-部署远程访问服务器时，有两种可用的拓扑：

    -   **两个适配器**-包含两个网络适配器，可以使用一个直接连接到 Internet 的网络适配器配置远程访问，另一个网络适配器连接到内部网络。 或者将该服务器安装在边缘设备（如防火墙或路由器）的后面。 在此配置中，将一个网络适配器连接到外围网络，另一个连接到内部网络。

    -   **单网络适配器**-在此配置中，远程访问服务器安装在边缘设备（如防火墙或路由器）的后面。 网络适配器连接到内部网络。

-   **网络适配器**-启用 DirectAccess 向导会根据 VPN 使用的接口自动检测在远程访问服务器上配置的网络适配器。 必须确保已选择正确的适配器。

-   **ConnectTo 地址**-客户端计算机使用 ConnectTo 地址连接到远程访问服务器。 你选择的地址必须与你为 IP-HTTPS 连接部署的 IP-HTTPS 证书的使用者名称相匹配，并且必须在公用 DNS 中可用。 请参阅“规划 IP-HTTPS 的网站证书”。

-   Ip-https**证书**-如果配置了 sstp VPN，则启用 DirectAccess 向导将选取 SSTP 用于 ip-https 的证书。 如果未配置 SSTP VPN，则该向导将尝试检查是否已配置 IP-HTTPS 的证书。 如果未配置，它将为 IP-HTTPS 自动设置自签名证书。该向导将自动启用 Kerberos 身份验证。 该向导还将为仅 IPv4 环境中的协议转换启用 NAT64 和 DNS64。

-   **IPv6 前缀**-如果向导检测到已在网络适配器上部署 ipv6，则它会自动创建内部网络的 ipv6 前缀、要分配到 DirectAccess 客户端计算机的 ipv6 前缀，以及要分配给 VPN 客户端计算机的 ipv6 前缀。 如果为本机 IPv6 或 ISATAP 基础结构自动生成的前缀不正确，你必须手动更改它们。 请参阅 1.1 规划网络和服务器拓扑和设置。

-   **Windows 7 客户**端-默认情况下，windows 7 客户端计算机无法连接到 windows Server 2012 远程访问部署。 如果你的组织中的 Windows 7 客户端计算机需要远程访问内部资源，你可以允许它们进行连接。 任何你要允许访问内部资源的客户端计算机都必须是启用 DirectAccess 向导中指定的安全组的成员。

    > [!NOTE]
    > 允许 Windows 7 客户端计算机使用 DirectAccess 进行连接需要你使用计算机证书身份验证。

-   **身份验证**-启用 DirectAccess 向导使用 Active Directory 对用户凭据进行身份验证。 若要部署双重身份验证，请参阅[部署带有 OTP 身份验证的远程访问](../../ras/otp/Deploy-RA-OTP.md)。





