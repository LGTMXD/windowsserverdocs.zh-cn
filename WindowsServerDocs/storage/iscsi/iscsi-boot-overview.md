---
ms.assetid: 134840f3-c416-4a10-ad73-ef7855b206f7
title: iSCSI 目标启动概述
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: f3f2ce63afa3e75b6d2f55789866c1872504c8eb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957414"
---
# <a name="iscsi-target-boot-overview"></a>iSCSI 目标启动概述

> 适用于：Windows Server 2016

Windows Server 中的 iSCSI 目标服务器可以从存储在集中位置的一个操作系统映像启动数百台计算机。 这样可提高效率、可管理性、可用性以及安全性。

## <a name="feature-description"></a><a name="BKMK_OVER"></a>功能说明
通过使用差异虚拟硬盘 \( vhd \) ，你可以使用一个操作系统映像（ \( "主映像"） \) 启动多达256台计算机。 例如，假设你使用大约为 20 GB 的操作系统映像部署了 Windows Server，并且你使用了两个镜像磁盘驱动器充当启动卷。 你需要将大约 10 TB 的存储仅用于操作系统映像来启动 256 台计算机。 借助 iSCSI 目标服务器，你会对操作系统基本映像使用 40 GB，对每个服务器实例的差异虚拟硬盘使用 2 GB，从而对操作系统映像总计使用 552 GB。 这样仅在操作系统映像存储方面就节省了 90% 以上。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>实际的应用程序
使用受控的操作系统映像具有以下优点：

**更安全且更易于管理。** 某些企业要求通过在中央位置以物理方式锁定存储来保护数据。 在这种方案中，服务器远程访问数据，包括操作系统映像。 借助 iSCSI 目标服务器，管理员可以集中管理操作系统启动映像，并且可以控制要用于主映像的应用程序。

**快速部署。** 由于主映像是使用 Sysprep 准备的，因此当计算机从主映像启动时，它们会跳过在 Windows 安装期间发生的文件复制和安装阶段，从而直接进入自定义阶段。 在 Microsoft 内部测试中，256 台计算机可在 34 分钟内进行部署。

**快速恢复。** 由于操作系统映像在运行 iSCSI 目标服务器的计算机上承载，因此如果需要替换无磁盘客户端，则新计算机可以指向该操作系统映像并立即启动。

> [!NOTE]
> 各种供应商都提供了存储区域网络 \(SAN\) 启动解决方案，可供 Windows Server 中的 iSCSI 目标服务器在商用硬件上使用。

## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>硬件要求
iSCSI 目标服务器不需要特殊硬件即可完成功能验证。 在具有大型部署的数据中心，应根据特定硬件对设计进行验证。 作为参考，Microsoft 内部测试表明，256计算机部署需要 \- 在 RAID 10 配置中将 RPM 磁盘24x15k-rpm 为存储。 网络带宽最好为 10 GB。 一般估计每 1 GB 网络适配器 60 个 iSCSI 启动服务器。

此方案无需网络适配器，可以使用软件启动加载程序（如 iPXE 开源启动固件）。

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>软件要求
iSCSI 目标服务器可以作为“文件和 iSCSI 服务”角色服务的一部分安装在服务器管理器中。

> [!NOTE]
> 不支持从 iSCSI（Windows iSCSI 目标服务器或第三方目标实现）启动 Nano Server。

## <a name="additional-references"></a>其他参考
* [iSCSI 目标服务器](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh848272(v=ws.11))
* [iSCSI 发起程序 cmdlet](/powershell/module/iscsi/?view=win10-ps)
* [iSCSI 目标服务器概述](/powershell/module/iscsi/?view=win10-ps)
