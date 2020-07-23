---
title: DFS 命名空间概述
ms.prod: windows-server
ms.author: jgerend
manager: daveba
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 06/07/2019
description: 本主题介绍 DFS 命名空间，这是 Windows Server 中的一个角色服务，可用于将不同服务器上的共享文件夹组合到一个或多个逻辑结构的命名空间中。
ms.openlocfilehash: 57d2d8bb7565677afcd2a031807061ab50b6ff16
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964089"
---
# <a name="dfs-namespaces-overview"></a>DFS 命名空间概述

> 适用于：Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server（半年频道）

DFS 命名空间是 Windows Server 中的一种角色服务，支持你将位于不同服务器的共享文件夹组合到一个或多个逻辑结构的命名空间。 如此可以为用户提供共享文件夹的虚拟视图，其中一条路径可转至位于多个服务器上的文件，具体如下图所示：

![DFS 命名空间技术元素](media/dfs-overview.png)

以下说明了 DFS 命名空间的组成元素：

- **命名空间服务器** - 命名空间服务器承载命名空间。 命名空间服务器可以是成员服务器或域控制器。
- **命名空间根路径** - 命名空间根路径是命名空间的起点。 在上图中，根的名称为 Public，命名空间路径为 \\ \\ Contoso \\ Public。 此类型命名空间是基于域的命名空间，因为它以域名开头（例如 Contoso），并且其元数据存储在 Active Directory 域服务 (AD DS) 中。 尽管上图显示了单个命名空间服务器，但是基于域的命名空间可以存放在多个命名空间服务器上，以提高命名空间的可用性。
- **文件夹** - 没有文件夹目标的文件夹将结构和层次结构添加到命名空间，具有文件夹目标的文件夹为用户提供实际内容。 用户浏览命名空间中具有文件夹目标的文件夹时，客户端计算机将收到将客户端计算机透明地重定向到一个文件夹目标的引荐。
- **文件夹目标** - 文件夹目标是共享文件夹或与命名空间中的某个文件夹关联的另一个命名空间的 UNC 路径。 文件夹目标是存储数据和内容的位置。 在上图中，名为 Tools 的文件夹包含两个文件夹目标，一个位于伦敦，一个位于纽约，名为 Training Guides 的文件夹包含一个文件夹目标，位于纽约。 浏览到 \\ \\ Contoso \\ 公共 \\ 软件工具的用户 \\ 以透明方式重定向到共享文件夹 \\ \\ LDN-SVR \\ 工具或 \\ \\ NYC-SVR \\ 工具，具体取决于用户当前所在的站点。

本主题讨论如何安装 DFS、新增功能，以及在哪里可以找到评估和部署信息。

可以使用 DFS 管理、[Windows PowerShell 中的 DFS 命名空间 (DFSN) Cmdlet](/powershell/module/dfsn/?view=win10-ps)、**DfsUtil** 命令或调用 WMI 的脚本来管理命名空间。

## <a name="server-requirements-and-limits"></a>服务器要求和限制

运行 DFS 管理或使用 DFS 命名空间没有其他硬件或软件要求。

命名空间服务器是承载命名空间的域控制器或成员服务器。 服务器上可以承载的命名空间数量取决于命名空间服务器上运行的操作系统。

除了单个独立命名空间之外，运行下列操作系统的服务器还可以承载多个基于域的命名空间。

- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 Datacenter 和 Enterprise Edition
- Windows Server（半年频道）

运行下列操作系统的服务器可以承载单个独立命名空间：

- Windows Server 2008 R2 Standard

下表描述了在选择要承载命名空间的服务器时需要考虑的其他因素。

| 承载独立命名空间的服务器 | 承载基于域的命名空间的服务器 |
| ---                                   |        ---                                |
| 必须包含一个 NTFS 卷以承载命名空间。|必须包含一个 NTFS 卷以承载命名空间。 |
| 可以是成员服务器或域控制器。|必须是命名空间配置时所在域中的成员服务器或域控制器。 （此要求适用于每个承载既定基于域的命名空间的命名空间服务器。） |
| 可以通过故障转移群集承载以提高命名空间的可用性。|命名空间不得为故障转移群集中的群集资源。 但是，如果将命名空间配置为仅使用充当故障转移群集中节点的服务器上的本地资源，则可以在该服务器上定位命名空间。 |

## <a name="installing-dfs-namespaces"></a>安装 DFS 命名空间

DFS 命名空间和 DFS 复制是文件和存储服务角色中的一部分。 DFS 的管理工具（DFS 管理、Windows PowerShell 的 DFS 命名空间模块及命令行工具）分别安装为远程服务器管理工具的一部分。

使用[Windows 管理中心](../../manage/windows-admin-center/overview.md)、服务器管理器或 POWERSHELL 安装 DFS 命名空间，如下一节中所述。

### <a name="to-install-dfs-by-using-server-manager"></a>使用服务器管理器安装 DFS 的步骤

1. 打开服务器管理器，单击 **“管理”** ，然后单击 **“添加角色和功能”** 。 将出现“添加角色和功能向导”。

2. 在 **“服务器选择”** 页面上，选择你想要在其上安装 DFS 的脱机虚拟机的服务器或虚拟硬盘 (VHD)。

3. 选择要安装的角色服务和功能。

    - 若要安装 DFS 命名空间服务，请在**服务角色**页上选择 **DFS 命名空间**。

    - 若只安装 DFS 管理工具，请在 **“功能”** 页上，展开 **“远程服务器管理工具”** 、 **“角色管理工具”** 、 **“文件服务工具”** ，然后选择 **“DFS 管理工具”** 。

         **“DFS 管理工具”** 安装 DFS 管理管理单元、Windows PowerShell 的 DFS 命名空间模块和命令行工具，但它不在服务器上安装任何 DFS 服务。

### <a name="to-install-dfs-by-using-windows-powershell"></a>使用 Windows PowerShell 安装 DFS 的步骤

使用提升的用户权限打开 Windows PowerShell 会话，然后键入以下命令，其中 <name\> 是你想要安装的角色服务或功能（请参阅下表获取一列相关角色服务或功能名称）：

```PowerShell
Install-WindowsFeature <name>
```

| 角色服务或功能 | 名称 |
| ----------------------- | ---- |
| DFS 命名空间          | `FS-DFS-Namespace` |
| DFS 管理工具    | `RSAT-DFS-Mgmt-Con` |

例如，若要安装远程服务器管理工具功能中的分布式文件系统工具部分，请键入：

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

若要安装 DFS 命名空间和远程服务器管理工具功能中的分布式文件系统工具部分，请键入：

```PowerShell
Install-WindowsFeature "FS-DFS-Namespace", "RSAT-DFS-Mgmt-Con"
```

## <a name="interoperability-with-azure-virtual-machines"></a>Azure 虚拟机的互操作性

在 Microsoft Azure 中的虚拟机上使用 DFS 命名空间已经过测试；但是，有一些必须遵循的限制和要求。

- 你不能在 Azure 虚拟机中对独立命名空间进行群集。

- 可以在 Azure 虚拟机中承载基于域的命名空间，包括 Azure Active Directory 的环境。

若要了解如何开始使用 Azure 虚拟机，请参阅 [Azure 虚拟机文档](/azure/virtual-machines/)。

## <a name="additional-references"></a>其他参考

有关其他相关信息，请参阅以下资源。

| 内容类型        | 参考 |
| ------------------  | ----------------|
| **产品评估** | [Windows Server 中 DFS 命名空间和 DFS 复制的新增功能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn281957(v=ws.11)) |
| **部署**    | [DFS 命名空间可扩展性注意事项](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) |
| **操作**    | [DFS 命名空间：常见问题](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee404780(v=ws.10)) |
| **社区资源** | [文件服务和存储 TechNet 论坛](https://social.technet.microsoft.com/forums/winserverfiles/threads/) |
| **协议**        | [Windows Server 中的文件服务协议](/openspecs/windows_protocols/MS-WINPROTLP/df36f95e-6a6b-48d6-a3ae-35a17674f546)（不推荐使用） |
| **相关技术** | [故障转移群集](../../failover-clustering/failover-clustering-overview.md)|
| **支持** | [Windows IT 专业人员支持](https://www.microsoft.com/itpro/windows/support)|
