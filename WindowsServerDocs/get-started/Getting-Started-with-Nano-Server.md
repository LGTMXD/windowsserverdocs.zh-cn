---
title: 安装 Nano Server
description: 干净安装、升级、迁移和评估 Nano Server
manager: dougkim
ms.date: 09/06/2017
ms.topic: get-started-article
ms.assetid: 2c2fa45b-6f3b-4663-b421-2da6ecc463bf
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 56944f3672a2caccb208aef4b2db465f354ad528
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990556"
---
# <a name="install-nano-server"></a>安装 Nano Server

>适用于：Windows Server 2016

> [!IMPORTANT]
> 自 Windows Server 版本 1709 开始，Nano Server 将仅用作[容器基本 OS 映像](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)。 查看[对 Nano Server 进行的更改](nano-in-semi-annual-channel.md)以了解其含义。

Windows Server 2016 提供了新的安装选项：Nano Server。 Nano Server 是针对私有云和数据中心进行优化的远程管理的服务器操作系统。 它类似于服务器核心模式中的 Windows Server，但显著变小，无本地登录功能，且仅支持 64 位应用程序、工具和代理。 其所需的磁盘空间更小，启动速度明显更快，且所需的更新和重启操作远远少于 Windows Server。 当它未重新启动时，则可以更快地重新启动。 Nano Server 安装选项仅适用于 Windows Server 2016 的 Standard 和 Datacenter 版本。

Nano Server 非常适合于多种方案：

-   作为 Hyper-V 虚拟机的计算主机，无论是否在群集中

-   作为横向扩展文件服务器的存储主机。

-   作为 DNS 服务器

-   作为运行 Internet Information Services (IIS) 的 Web 服务器

-   作为使用云应用程序模式开发以及在容器或虚拟机来宾操作系统中运行的应用程序的主机

## <a name="important-differences-in-nano-server"></a>Nano Server 中的重要差异

因为 Nano Server 经过优化，是轻量操作系统（运行基于容器和微服务的云-本机应用程序）或者敏捷且经济高效的数据中心主机（空间占用显著减少），因此 Nano Server 与“服务器核心”或“具有桌面体验安装的服务器”安装间存在重要差异：

- Nano Server 无外设；没有任何本地登录功能或图形用户界面。
- 仅支持 64 位应用程序、工具和代理。
- Nano Server 无法充当 Active Directory 域控制器。
- 不支持组策略。 但是，可以使用[所需状态配置](/previous-versions/dn387184(v=vs.85))大规模应用设置。
- 不能将 Nano Server 配置为使用代理服务器访问 Internet。
- 不支持 NIC 组合（特别是负载平衡和故障转移或 LBFO）。 但支持开关嵌入组合 (SET)。
- 不支持 Microsoft Endpoint Configuration Manager 和 System Center Data Protection Manager。
- 不支持最佳做法分析器 (BPA) cmdlet 以及 BPA 与服务器管理器的集成。
- Nano Server 不支持虚拟主机总线适配器 (HBA)。
- Nano Server 不需要使用产品密钥激活。 Nano Server 充当 Hyper-V 主机时不支持[自动虚拟机激活](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303421(v=ws.11)) (AVMA)。 通过将[密钥管理服务](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612867(v=ws.11)) (KMS) 与通用批量许可证密钥配合使用，或者使用[基于 Active Directory 的激活](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502534(v=ws.11))，可以激活 Nano Server 主机上运行的虚拟机。
- 随 Nano Server 附带提供的 Windows PowerShell 版本具有重要差异。 有关详细信息，请参阅 [Nano Server上的 PowerShell](PowerShell-on-Nano-Server.md)。
- 仅在 Current Branch for Business (CBB) 模型上支持 Nano Server -- 目前不存在 Long Term Servicing Branch (LTSB) 版本的 Nano Server。 有关详细信息，请参阅下列各子节。

### <a name="current-branch-for-business"></a>Current Branch for Business
Nano Server 拥有一个更活跃的模型，称为 Current Branch for Business (CBB)，通过快速开发周期对以云节奏移动的客户提供支持。 在此模型中，Nano Server 的功能更新发布每年会有两到三次。 这种模型要求生产中部署和运行的 Nano Server 具有[软件保障](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx)。 若要维持支持，管理员不得滞后两次以上的 CBB 发布。 但是，这些版本不会自动更新现有部署；管理员在方便时手动安装新的 CBB 版本。 更多信息，请参阅 [Windows Server 2016 new Current Branch for Business servicing option](https://cloudblogs.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/)（新的 Windows Server 2016 Current Branch for Business 服务选项）。

“服务器核心”和“具有桌面体验的服务器”安装选项仍然以 [Long Term Servicing Branch (LTSB) 模型](https://support.microsoft.com/lifecycle#gp%2Fgp_msl_policy)为服务基础，包含 5 年的主流支持和 5 年的扩展支持。

## <a name="installation-scenarios"></a>安装方案

### <a name="evaluation"></a>评估
可以从 [Windows Server 评估](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)获取 Windows Server 的 180 天许可证评估副本。 若要试用 Nano Server，请选择“Nano Server”|“64 位 EXE 选项”  ，然后返回到[Nano Server 快速启动](Nano-Server-Quick-Start.md)或[部署 Nano Server](Deploy-Nano-Server.md)开始试用。

### <a name="clean-installation"></a>全新安装
因为通过配置 VHD 安装 Nano Server，所以干净安装是最快和最简单的部署方法。

- 若要使用 DHCP 快速开始 Nano Server 的基本部署来获取 IP 地址，请参阅 [Nano Server 快速启动](Nano-Server-Quick-Start.md)
- 如果已经熟悉 Nano Server 的基础知识，开头为[部署 Nano Server](Deploy-Nano-Server.md) 的较为详细的主题提供有关进行自定义映像、使用域、联机与脱机安装服务器角色的程序包和其他功能等的一套完整说明。

> [!IMPORTANT]
> 完成安装后，如果已安装所需的所有服务器角色和功能，则可以立即检查并安装 Windows Server 2016 可用的更新。 对于 Nano Server，请参阅[管理 Nano Server](Manage-Nano-Server.md) 的“管理 Nano Server 中的更新”部分。

### <a name="upgrade"></a>升级
由于 Nano Server 是 Windows Server 2016 的新增功能，所以还没有从旧操作系统版本到 Nano Server 的升级路径。

### <a name="migration"></a>迁移
由于 Nano Server 是 Windows Server 2016 的新增功能，所以还没有从旧操作系统版本到 Nano Server 的迁移路径。

-------------------------------------
如果需要不同的安装选项，可以[返回至 Windows Server 2016 主页](../index.yml)