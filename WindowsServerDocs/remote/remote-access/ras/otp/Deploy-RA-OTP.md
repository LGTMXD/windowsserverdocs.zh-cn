---
title: 部署带有 OTP 身份验证的远程访问
description: 本主题是指南使用 Windows Server 2016 中的 "使用 OTP 身份验证部署远程访问" 指南的一部分。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: b1b2fe70-7956-46e8-a3e3-43848868df09
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d1b38f753e2e4d8333299c369042a72e0dc3a6e6
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182003"
---
# <a name="deploy-remote-access-with-otp-authentication"></a>部署带有 OTP 身份验证的远程访问

>适用于：Windows Server（半年频道）、Windows Server 2016

 Windows Server 2016 和 Windows Server 2012 将 DirectAccess 和路由以及远程访问服务 \( RRAS \) VPN 合并到单个远程访问角色中。

## <a name="scenario-description"></a><a name="BKMK_OVER"></a>方案描述
在此方案中，已将启用 DirectAccess 的远程访问服务器配置为使用两个因素一次性密码 OTP 身份验证对 DirectAccess 客户端用户进行身份 \- \( \) 验证，以及标准 Active Directory 凭据。

## <a name="prerequisites"></a>先决条件
在开始部署此方案之前，请查看此列表以了解重要要求：

-   部署 OTP 之前，必须先部署[具有高级设置的单个 DirectAccess 服务器](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)。

-   Windows 7 客户端必须使用 DCA 2.0 支持 OTP。

-   OTP 不支持更改 PIN 更改。

-   必须部署公钥基础结构。

    有关详细信息，请参阅： [测试实验室指南微型模块：用于 Windows Server 2012 的基本 PKI。](https://docs.microsoft.com/answers/topics/windows-server-2012.html)

-   不支持在 DirectAccess 管理控制台或 Windows PowerShell cmdlet 之外更改策略。

## <a name="in-this-scenario"></a>本方案内容
OTP 身份验证方案包含许多步骤：

1.  [使用高级设置部署单个 DirectAccess 服务器](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)。 配置 OTP 之前，必须先部署单个远程访问服务器。 计划和部署单台服务器包括设计和配置网络拓扑、计划和部署证书、设置 DNS 和 Active Directory、配置远程访问服务器设置、部署 DirectAccess 客户端以及准备 Intranet 服务器。

2.  [使用 OTP 身份验证规划远程访问](./plan/plan-remote-access-with-otp-authentication.md)。 除了单个服务器所需的规划外，OTP 还要求规划 Microsoft 证书颁发机构 \( CA \) 和 otp 证书模板以及启用 RADIUS 的 \- otp 服务器。 计划可能还包括安全组的要求，以使特定用户免于使用强 \( OTP 或智能卡 \) 身份验证。 有关在多林环境中配置 OTP 的信息 \- ，请参阅[配置多林部署](../../ras/multi-forest/Configure-a-Multi-Forest-Deployment.md)。

3.  [配置具有 OTP 身份验证的 DirectAccess](/configure/Configure-RA-with-OTP-Authentication.md)。 OTP 部署包含多个配置步骤，包括准备用于 OTP 身份验证的基础结构，配置 OTP 服务器，在远程访问服务器上配置 OTP 设置，以及更新 DirectAccess 客户端设置。

4.  [对 OTP 部署进行故障排除]((/troubleshoot/Troubleshoot-an-OTP-Deployment.md). 此故障排除部分介绍了使用 OTP 身份验证部署远程访问时可能出现的一些最常见的错误。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>实际的应用程序
提高安全性-使用 OTP 增加了 DirectAccess 部署的安全性。 用户需要 OTP 凭据才能访问内部网络。 用户通过 Windows 10 或 Windows 8 客户端计算机上的网络连接中可用的工作区连接提供 OTP 凭据，或通过使用 \( \) 运行 Windows 7 的客户端计算机上的 DirectAccess 连接助手 DCA 提供 OTP 凭据。 OTP 身份验证过程包括以下步骤：

1.  DirectAccess 客户端输入域凭据， \( 通过基础结构隧道访问 DirectAccess 基础结构服务器 \) 。  如果由于特定的 IKE 故障导致内部网络的连接不可用，则客户端计算机上的工作区连接将通知用户需要输入凭据。 在运行 Windows 7 的客户端计算机上， \- 会出现请求智能卡凭据的弹出窗口。

2.  输入 OTP 凭据后，这些凭据将通过 SSL 发送到远程访问服务器，同时提供对短期 \- 智能卡登录证书的请求。

3.  远程访问服务器使用基于 RADIUS 的 OTP 服务器启动对 OTP 凭据的验证 \- 。

4.  如果通过验证，远程访问服务器会使用其注册机构证书对证书请求签名，并将其发送回 DirectAccess 客户端计算机

5.  DirectAccess 客户端计算机将已签名的证书请求转发到 CA，并存储注册的证书以供 Kerberos SSP \/ AP 使用。

6.  使用本证书，客户端计算机能够以透明方式执行标准的智能卡 Kerberos 身份验证。

## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>本方案所包括的角色和功能
下表列出了本方案所需的角色和功能：

|角色 \/ 功能|如何支持本方案|
|---------|-----------------|
|*远程访问管理角色*|该角色可使用服务器管理器控制台加以安装和卸载。 此角色包括 DirectAccess （以前是 Windows Server 2008 R2 中的一项功能）以及路由和远程访问服务（以前是网络策略和访问服务 \( NPAS 服务器角色下的角色服务） \) 。 远程访问角色由以下两个组件组成：<p>1. DirectAccess 和路由和远程访问服务 \( RRAS \) VPN-DIRECTACCESS 和 VPN 在远程访问管理控制台中一起进行管理。<br />2. RRAS 路由-RRAS 路由功能在旧版路由和远程访问控制台中进行管理。<p>远程访问角色取决于以下服务器功能：<p>-Internet Information Services \( IIS \) Web 服务器-需要此功能来配置网络位置服务器、使用 OTP 身份验证和配置默认 Web 探测。<br />-Windows 内部数据库-用于远程访问服务器上的本地记帐。|
|远程访问管理工具功能|此功能的安装如下所述：<p>-在安装远程访问角色时，它默认安装在远程访问服务器上，并支持远程管理控制台用户界面。<br />-可选择将它安装在不运行远程访问服务器角色的服务器上。 在这种情况下，它可用于远程管理运行 DirectAccess 和 VPN 的远程访问计算机。<p>远程访问管理工具功能包括以下各项：<p>-远程访问 GUI 和命令行工具<br />-适用于 Windows PowerShell 的远程访问模块<p>依赖项包括：<p>-组策略管理控制台<br />-RAS 连接管理器管理工具包 \( CMAK\)<br />-Windows PowerShell 3。0<br />-图形管理工具和基础结构|

## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>硬件要求
本方案的硬件要求包括以下各项：

-   满足 Windows Server 2016 或 Windows Server 2012 硬件要求的计算机。

-   若要测试该方案，必须至少有一台运行 Windows 10、Windows 8 或 Windows 7 的计算机配置为 DirectAccess 客户端。

-   通过 RADIUS 支持 PAP 的 OTP 服务器。

-   OTP 硬件或软件令牌。

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>软件要求
存在许多对本方案的要求。

1.  对单台服务器部署的软件要求。 有关详细信息，请参阅[使用高级设置部署单个 DirectAccess 服务器](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)。

2.  除单台服务器的软件要求外，还存在许多特定于 OTP 的 \- 要求：

    1.  用于 IPsec 身份验证的 CA-在 OTP 部署中，必须使用 CA 颁发的 IPsec 计算机证书部署 DirectAccess。 OTP 部署不支持将远程访问服务器用作 Kerberos 代理的 IPsec 身份验证。 需要内部证书颁发机构。

    2.  用于 OTP 身份验证的 CA- \( 在 Windows 2003 服务器或更高版本上运行的 Microsoft 企业 CA \) 需要颁发 OTP 客户端证书。 可采纳颁发用于 IPsec 身份验证的证书的相同证书颁发机构。 必须可通过第一个基础结构隧道访问 CA 服务器。

    3.  安全组-若要免除用户的强身份验证，需要包含这些用户的 Active Directory 安全组。

    4.  客户端 \- 要求-对于 Windows 10 和 windows 8 客户端计算机，网络连接助手 \( NCA \) 服务用于检测是否需要 OTP 凭据。 如果是，DirectAccess 媒体管理器会提示输入凭据。  NCA 包含在操作系统中，无需安装或部署。 对于 Windows 7 客户端计算机，DirectAccess 连接助手 \( DCA \) 2.0 是必需的。 可从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=29039)下载该服务。

    5.  注意以下事项：

        1.  OTP 身份验证可与智能卡和受信任的平台模块 \( 基于 TPM 的 \) \- 身份验证并行使用。 在远程访问管理控制台中启用 OTP 身份验证的同时还将启用智能卡身份验证。

        2.  在远程访问配置期间，指定安全组中的用户可以从双重 \- 身份验证中免除，因此只能使用用户名密码进行身份验证 \/ 。

        3.  不支持 OTP 新的 PIN 和下一个令牌代码模式

        4.  在远程访问多站点部署中，OTP 设置是通用的，并是所有入口点的标识。 如果为 OTP 配置多台 RADIUS 或颁发证书机构服务器，则由每台远程访问服务器根据可用性和可伸缩性对这些服务器进行排序。

        5.  在远程访问多林环境中配置 OTP 时 \- ，Otp ca 只能来自资源林，并且应跨林信任配置证书注册。 有关更多信息，请参阅 [AD CS：Windows Server 2008 R2 上的跨林证书注册](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff955842(v=ws.10))。

        6.  使用 KEY FOB OTP 令牌的用户应在 DirectAccess OTP 对话框中插入 PIN，后跟 \( 不带任何分隔符的令牌 \) 。 使用 PIN PAD OTP 的用户应仅在对话的令牌代码当中插入 PIN。

        7.  启用 WEBDAV 时不应启用 OTP。

## <a name="known-issues"></a><a name="KnownIssues"></a>已知问题
下面是配置 OTP 方案时的已知问题：

-   远程访问使用探测机制来验证与基于 RADIUS 的 OTP 服务器之间的连接性 \- 。 在某些情况下，这可能会导致在 OTP 服务器上引发错误。 为了避免此问题，请在 OTP 服务器上执行以下操作：

    -   创建一个用户帐户，该帐户与在远程访问服务器上为探测机制配置的用户名和密码匹配。 用户名不应定义 Active Directory 用户。

        默认情况下，远程访问服务器上的用户名为 DAProbeUser，密码为 DAProbePass。 可使用远程访问服务器上注册表中的以下值来修改这些默认设置：

        -   HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ DirectAccess \\ OTP \\ RadiusProbeUser

        -   HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ DirectAccess \\ OTP \\ RadiusProbePass

-   如果更改已配置且正在运行的 DirectAccess 部署中的 IPsec 根证书，OTP 将停止工作。 若要解决此问题，请在每个 DirectAccess 服务器上的 Windows PowerShell 提示符下运行以下命令：`iisreset`

