---
title: 存储迁移服务概述
description: 利用存储迁移服务，可以更轻松地将存储迁移到 Windows Server 或 Azure。 它提供了一个图形工具，该工具在 Windows 和 Linux 服务器上对数据进行清点，然后将数据传输到较新的服务器或 Azure 虚拟机。 存储迁移服务还提供了将服务器标识传输到目标服务器的选项，以便应用和用户可以在不更改链接或路径的情况下访问其数据。
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 03/26/2020
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: 1403e0ecd12c4c15924781d75bd9127874018451
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953889"
---
# <a name="storage-migration-service-overview"></a>存储迁移服务概述

>适用于： Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server （半年频道）

利用存储迁移服务，可以更轻松地将存储迁移到 Windows Server 或 Azure。 它提供了一个图形工具，该工具在 Windows 和 Linux 服务器上对数据进行清点，然后将数据传输到较新的服务器或 Azure 虚拟机。 存储迁移服务还提供了将服务器标识传输到目标服务器的选项，以便应用和用户可以在不更改链接或路径的情况下访问其数据。

本主题讨论为何要使用存储迁移服务，迁移过程的工作方式、源服务器和目标服务器的要求，以及[存储迁移服务中的新增功能](#whats-new-in-storage-migration-service)。

## <a name="why-use-storage-migration-service"></a>为什么使用存储迁移服务

使用存储迁移服务，因为你有要迁移到较新的硬件或虚拟机的一台或多台服务器。 存储迁移服务旨在帮助你执行以下操作：

- 清点多个服务器及其数据
- 快速传输源服务器中的文件、文件共享和安全配置
- （可选）接管源服务器的标识（也称为 "剪切"），以便用户和应用无需更改任何内容即可访问现有数据
- 管理来自 Windows 管理中心用户界面的一个或多个迁移

![显示存储迁移服务将文件从源服务器迁移到目标服务器、Azure Vm 或 Azure 文件同步 & 配置的示意图。](media/overview/storage-migration-service-diagram.png)

**图1：存储迁移服务源和目标**

## <a name="how-the-migration-process-works"></a>迁移过程的工作方式

迁移过程分为三个步骤：

1. **列出服务器的清单**，收集有关其文件和配置的信息（如图2所示）。
2. 将数据从源服务器**传输（复制）** 到目标服务器。
3. **剪切到新服务器**（可选）。<br>目标服务器采用源服务器以前的标识，以便应用和用户无需更改任何内容。 <br>源服务器进入维护状态，其中仍包含它们始终包含的相同文件（我们永远不会从源服务器中删除文件），但对用户和应用不可用。 然后，你可以在方便的时候停止服务器。

![显示准备扫描的服务器的屏幕截图 ](media/migrate/inventory.png)
 **图2：存储迁移服务清点服务器**

下面的视频演示如何使用存储迁移服务来获取服务器（如现在不支持的 Windows Server 2008 R2 服务器），并将存储移到较新的服务器。

> [!VIDEO https://www.youtube.com/embed/h-Xc9j1w144]

## <a name="requirements"></a>要求

若要使用存储迁移服务，需要以下各项：

- 要从其迁移文件和数据的**源服务器**或**故障转移群集**
- 运行 Windows Server 2019 （群集或独立版）以迁移到的**目标服务器**。 Windows Server 2016 和 Windows Server 2012 R2 也工作正常，但速度低于50%
- 运行 Windows Server 2019 以管理迁移的**orchestrator 服务器**  <br>如果要仅迁移几个服务器，并且其中一个服务器正在运行 Windows Server 2019，则可以将其用作 orchestrator。 如果要迁移多个服务器，我们建议使用单独的 orchestrator 服务器。
- **运行[Windows 管理中心](../../manage/windows-admin-center/overview.md)的 PC 或服务器**运行存储迁移服务用户界面，除非您更愿意使用 PowerShell 来管理迁移。 Windows 管理中心和 Windows Server 2019 版本必须至少为版本1809。

强烈建议 orchestrator 和 destination 计算机至少有两个核心或两个个 vcpu，至少有 2 GB 的内存。 对于更多的处理器和内存，清单和传输操作的速度要快得多。

### <a name="security-requirements-the-storage-migration-service-proxy-service-and-firewall-ports"></a>安全要求、存储迁移服务代理服务和防火墙端口

- 作为源计算机和 orchestrator 计算机上的管理员的迁移帐户。
- 一个迁移帐户，它是目标计算机和 orchestrator 计算机上的管理员。
- Orchestrator 计算机*必须启用 "* 文件和打印机共享（SMB）" 防火墙规则。
- 源计算机和目标计算机必须启用以下防火墙规则*入站*（尽管可能已启用这些规则）：
  - 文件和打印机共享 (SMB-In)
  - Netlogon 服务（NP-IN）
  - Windows Management Instrumentation (DCOM-In)
  - Windows Management Instrumentation (WMI-In)

  > [!TIP]
  > 在 Windows Server 2019 计算机上安装存储迁移服务代理服务会自动在该计算机上打开所需的防火墙端口。 为此，请在 Windows 管理中心中连接到目标服务器，然后前往**服务器管理器**（在 Windows 管理中心中） >**角色和功能**"，选择"**存储迁移服务代理**"，然后选择"**安装**"。


- 如果计算机属于某个 Active Directory 域服务域，则它们应属于同一林。 如果要在剪切时将源的域名传输到目标，则目标服务器也必须与源服务器位于同一域中。 切换技术跨域运行，但目标的完全限定域名将不同于源 .。。

### <a name="requirements-for-source-servers"></a>源服务器的要求

源服务器必须运行以下操作系统之一：

- Windows Server 半年频道
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- Windows 2008 Server
- Windows Server 2003 R2
- Windows Server 2003
- Windows Small Business Server 2003 R2
- Windows Small Business Server 2008
- Windows Small Business Server 2011
- Windows Server 2012 Essentials
- Windows Server 2012 R2 Essentials
- Windows Server 2016 Essentials
- Windows Server 2019 Essentials
- Windows Storage Server 2008
- Windows Storage Server 2008 R2
- Windows Storage Server 2012
- Windows Storage Server 2012 R2
- Windows Storage Server 2016

注意： Windows Small Business Server 和 Windows Server Essentials 是域控制器。 存储迁移服务目前无法从域控制器中剪切，但可以列出和传输文件。

如果 orchestrator 正在运行 Windows Server 1903 或更高版本，或者协调器运行的 Windows Server 的早期版本安装了[KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) ，则可以迁移以下附加源类型：

- 运行 Windows Server 2012、Windows Server 2012 R2、Windows Server 2016、Windows Server 2019 的故障转移群集
- 使用 Samba 的 Linux 服务器。 我们测试了以下内容：
    - CentOS 7
    - Debian GNU/Linux 8
    - RedHat Enterprise Linux 7。6
    - SUSE Linux Enterprise Server （SLES） 11 SP4
    - Ubuntu 16.04 LTS 和 12.04.5 LTS
    - Samba 4.8、4.7、4.3、4.2 和3。6

### <a name="requirements-for-destination-servers"></a>目标服务器的要求

目标服务器必须运行以下操作系统之一：

- Windows Server 半年频道
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

> [!TIP]
> 运行 Windows Server 2019 或 Windows Server、半年频道或更高版本的目标服务器的 Windows Server 早期版本的传输性能加倍。 此性能提高的原因是包含内置的存储迁移服务代理服务，该服务还将打开所需的防火墙端口（如果尚未打开）。

## <a name="azure-vm-migration"></a>Azure VM 迁移

Windows 管理中心版本1910允许你部署 Azure 虚拟机。 这会将 VM 部署集成到存储迁移服务中。 在部署工作负荷之前，无需在 Azure 门户中创建新的服务器和 Vm，并且可能缺少所需的步骤和配置-Windows 管理中心可以部署 Azure VM、配置其存储、将其加入域、安装角色，然后设置你的分布式系统。

   以下视频演示了如何使用存储迁移服务迁移到 Azure Vm。
   > [!VIDEO https://www.youtube-nocookie.com/embed/k8Z9LuVL0xQ]
   
如果要将虚拟机直接迁移到 Azure，而不迁移到更高版本的操作系统，请考虑使用 Azure Migrate。 有关详细信息，请参阅[Azure Migrate 概述](https://go.microsoft.com/fwlink/?linkid=2056064)。

## <a name="whats-new-in-storage-migration-service"></a>存储迁移服务中的新增功能

Windows 管理中心版本1910添加了部署 Azure 虚拟机的功能。 这会将 Azure VM 部署集成到存储迁移服务中。 有关详细信息，请参阅[AZURE VM 迁移](#azure-vm-migration)。

在 Windows Server、版本1903或更高版本或 Windows [server 的早期](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)版本上运行存储迁移服务器 orchestrator 时，以下新功能可用：

- 将本地用户和组迁移到新服务器
- 从故障转移群集迁移存储，迁移到故障转移群集，并在独立服务器和故障转移群集之间迁移
- 从使用 Samba 的 Linux 服务器迁移存储
- 使用 Azure 文件同步更轻松地将已迁移的共享同步到 Azure 中
- 迁移到 Azure 等新网络

## <a name="additional-references"></a>其他参考

- [使用存储迁移服务迁移文件服务器](migrate-data.md)
- [存储迁移服务常见问题（FAQ）](faq.md)
- [存储迁移服务的已知问题](known-issues.md)
