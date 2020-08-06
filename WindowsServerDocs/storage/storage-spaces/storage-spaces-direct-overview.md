---
title: 存储空间直通概述
ms.prod: windows-server
ms.author: cosdar
manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/24/2020
ms.assetid: 8bd0d09a-0421-40a4-b752-40ecb5350ffd
description: 概述存储空间直通，Windows Server 和 Azure Stack HCI 的一项功能，使你能够将具有内部存储的服务器加入软件定义的存储解决方案。
ms.localizationpriority: medium
ms.openlocfilehash: 3fd86a8465d2fef59ccce73fc473790682f0d180
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864318"
---
# <a name="storage-spaces-direct-overview"></a>存储空间直通概述

>适用于： Azure Stack HCI、Windows Server 2019、Windows Server 2016

空间存储直通使用具有本地连接驱动器的行业标准服务器来创建高度可用、高度可扩展的软件定义存储，其成本仅占传统 SAN 或 NAS 阵列的一小部分。 它的聚合或超聚合体系结构大大简化了采购和部署，同时还提供了缓存、存储层和擦除编码等功能，以及最新的硬件创新（例如 RDMA 联网和 NVMe 驱动器），提供了无与伦比的效率和性能。

存储空间直通包含在[AZURE STACK HCI](/azure-stack/hci/)、windows Server 2019 Datacenter、windows Server 2016 Datacenter 和[Windows Server 有问必答 preview 内部版本](https://insider.windows.com/for-business-getting-started-server/)中。

有关存储空间的其他应用程序，如共享 SAS 群集和独立服务器，请参阅[存储空间概述](overview.md)。 如果正在查找有关在 Windows 10 电脑上使用存储空间的信息，请参阅[windows 10 中的存储空间](https://support.microsoft.com/help/12438/windows-10-storage-spaces)。

| 说明 | 文档 |
|--|--|
| **了解**<br><ul><li>概述（你目前位于此位置）</li><li>[了解缓存](understand-the-cache.md)</li><li>[容错和存储效率](storage-spaces-fault-tolerance.md)<li>[驱动器对称注意事项](drive-symmetry-considerations.md)</li><li>[了解并监视存储重新同步](understand-storage-resync.md)</li><li>[了解群集和池仲裁](understand-quorum.md)</li><li>[群集集](cluster-sets.md)</li> | **计划**<br><ul><li>[硬件要求](storage-spaces-direct-hardware-requirements.md)</li><li>[使用 CSV 内存中读取缓存](csv-cache.md)</li><li>[选择驱动器](choosing-drives.md)</li><li>[规划卷](plan-volumes.md)</li><li>[使用来宾 VM 群集](storage-spaces-direct-in-vm.md)</li><li>[灾难恢复](storage-spaces-direct-disaster-recovery.md)</li> |
| **部署**<br><ul><li>[部署存储空间直通](deploy-storage-spaces-direct.md)</li><li>[创建卷](create-volumes.md)</li><li>[嵌套复原](nested-resiliency.md)</li><li>[配置仲裁](../../failover-clustering/manage-cluster-quorum.md)</li><li>[将存储空间直通群集升级为 Windows Server 2019](upgrade-storage-spaces-direct-to-windows-server-2019.md)</li><li>[了解和部署永久性内存](deploy-pmem.md)</li> | **管理**<br><ul><li>[使用 Windows Admin Center 管理](../../manage/windows-admin-center/use/manage-hyper-converged.md)</li><li>[添加服务器或驱动器](add-nodes.md)</li><li>[使服务器脱机以进行维护](maintain-servers.md)</li><li>[删除服务器](remove-servers.md)</li><li>[扩展卷](resize-volumes.md)</li><li>[删除卷](delete-volumes.md)</li><li>[更新驱动器固件](../update-firmware.md)</li><li>[性能历史记录](performance-history.md)</li><li>[分隔卷的分配](delimit-volume-allocation.md)</li><li>[在超聚合群集上使用 Azure Monitor](configure-azure-monitor.md)</li> |
| **疑难解答**<br><ul><li>[故障排除方案](troubleshooting-storage-spaces.md)</li><li>[运行状况和运行状态故障排除](storage-spaces-states.md)</li><li>[通过存储空间直通收集诊断数据](data-collection.md)</li><li>[存储类内存运行状况管理](Storage-class-memory-health.md)</li> | **最新博客文章**<br><ul><li>[13700000 IOPS 与存储空间直通：超聚合基础结构的新行业记录](https://techcommunity.microsoft.com/t5/storage-at-microsoft/the-new-hci-industry-record-13-7-million-iops-with-windows/ba-p/428314)</li><li>[Windows Server 2019 中的超聚合基础结构-立即开始倒计时时钟！](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)</li><li>[Windows Server 峰会发布五大大广告](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)</li><li>[10000存储空间直通分类和计数 .。。](https://techcommunity.microsoft.com/t5/storage-at-microsoft/storage-spaces-direct-10-000-clusters-and-counting/ba-p/428185)</li></ul> |

## <a name="videos"></a>视频

**快速视频概述 (5 分钟) **

> [!Video https://www.youtube-nocookie.com/embed/raeUiNtMk0E]

**Microsoft Ignite 2018 (1 小时存储空间直通) **

> [!Video https://www.youtube-nocookie.com/embed/5kaUiW3qo30]

**Microsoft Ignite 2017 (1 小时存储空间直通) **

> [!Video https://www.youtube-nocookie.com/embed/YDr2sqNB-3c]

**在 Microsoft Ignite 2016 (1 小时内启动事件) **

> [!Video https://www.youtube-nocookie.com/embed/LK2ViRGbWs]

## <a name="key-benefits"></a>主要优点

| 映像 | 描述 |
|--|--|
| ![简单](media/storage-spaces-direct-in-windows-server-2016/simplicity-icon.png) | **简易.** 在 15 分钟内即可从运行 Windows Server 2016 的行业标准服务器转到第一个存储空间直通群集。 对于 System Center 用户而言，部署不仅仅只是一个复选框。 |
| ![无与伦比的性能](media/storage-spaces-direct-in-windows-server-2016/performance-icon.png) | **无可匹敌的性能。** 无论是全闪存还是混合存储空间直通，都可以轻松超越[每台服务器 150,000 次混合 4K 随机 IOPS](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) 的限制，并且具有较高的一致性和较低的延迟，所有这一切均归功于其嵌入虚拟机监控程序的体系结构、内置的读/写缓存，以及对直接安装在 PCIe 总线上的尖端 NVMe 驱动器的支持。 |
| ![容错](media/storage-spaces-direct-in-windows-server-2016/fault-tolerance-icon.png) | **容错。** 具有内置的复原功能，可在不影响可用性的情况下处理驱动器、服务器或组件故障。 大规模部署还可以配置[机箱和机架容错](../../failover-clustering/fault-domains.md)。 如果硬件发生故障，只需更换发生故障的硬件，而软件会自行复原，不需要复杂的管理步骤。 |
| ![资源效率](media/storage-spaces-direct-in-windows-server-2016/efficiency-icon.png) | **资源效率。** 擦除编码最多可提高 2.4 倍的存储效率，它采用独特的创新（如本地重建代码和 ReFS 实时层），使效率优势扩展到了硬盘驱动器及热/冷混合工作负载，同时最大程度降低了 CPU 使用率，为最需要的设备（即 VM）提供资源。 |
| ![可管理性](media/storage-spaces-direct-in-windows-server-2016/manageability-icon.png) | **可管理性**。 使用[存储 QoS 控件](../storage-qos/storage-qos-overview.md)，使过于繁忙的 VM 保持符合每台 VM 的 IOPS 上限和下限。 [运行状况服务](../../failover-clustering/health-service-overview.md)提供连续的内置监视和警报，并使用新的 API，可在群集范围内轻松收集大量性能和容量指标。 |
| ![可伸缩性](media/storage-spaces-direct-in-windows-server-2016/scalability-icon.png) | **可伸缩性**。 可扩展到 16 台服务器以及超过 400 个驱动器，每个群集拥有最高 1 PB (1,000 TB) 的存储。 只需添加驱动器或添加更多服务器即可实现扩展，存储空间直通会自动载入新的驱动器，并开始使用它们。 存储效率和性能如预期大幅提升。 |

## <a name="deployment-options"></a>部署选项

存储空间直通适用于两种不同的部署选项：

### <a name="converged"></a>聚合

**单独群集中的存储和计算。** 聚合部署选项（也称为“分解部署”）将横向扩展文件服务器 (SoFS) 放在存储空间直通之上，通过 SMB3 文件共享提供网络连接存储。 它可以独立于存储群集扩展计算/工作负荷，服务提供商和企业的 Hyper-V IaaS（基础结构即服务）等大规模部署就需要采用这种部署。

![存储空间直通使用横向扩展文件服务器功能为另一个服务器或群集中的 Hyper-V VM 提供存储](media/storage-spaces-direct-in-windows-server-2016/converged-minimal.png)

### <a name="hyper-converged"></a>超聚合

**一个用于计算和存储的群集。** 超聚合部署选项直接在提供存储、在本地卷上存储文件的服务器上运行 Hyper-V 虚拟机或 SQL Server 数据库。 此部署选项无需配置文件服务访问和权限，降低了中小型企业或远程机构/分支机构部署的硬件成本。 请参阅[部署存储空间直通](deploy-storage-spaces-direct.md)。

![存储空间直通为同一群集中的 Hyper-V VM 提供存储](media/storage-spaces-direct-in-windows-server-2016/hyper-converged-minimal.png)

## <a name="how-it-works"></a>工作原理

存储空间直通由存储空间演变而来，最先在 Windows Server 2012 中引入。 它利用 Windows Server 中当前已知的许多功能，如故障转移群集、群集共享卷 (CSV) 文件系统、服务器消息块 (SMB) 3 以及存储空间。 它还引入了新技术，最值得注意的是软件存储总线。

下面部分概括介绍存储空间直通堆栈：

![存储空间直通堆栈](media/storage-spaces-direct-in-windows-server-2016/converged-full-stack.png)

**网络硬件。** 存储空间直通使用 SMB3（包括 SMB 直通和 SMB 多通道）通过以太网在服务器之间通信。 强烈建议使用具有远程直接内存访问 (RDMA) 的 10+ GbE（iWARP 或 RoCE）。

**存储硬件。** 2-16 台具有本地连接 SATA、SAS 或 NVMe 驱动器的服务器。 每台服务器至少必须有 2 个固态驱动器，至少 4 个其他驱动器。 SATA 和 SAS 设备应位于主机总线适配器 (HBA) 和 SAS 扩展器之后。 强烈建议使用合作伙伴提供的平台，这种平台经过精心设计并广泛验证，即将推出。

**故障转移群集。** Windows Server 的内置群集功能用于连接服务器。

**软件存储总线。** 存储空间直通中新增了软件存储总线。 它可以跨越群集，建立软件定义的存储构造，在这种构造中，所有服务器都可以相互看到对方的所有本地驱动器。 可以考虑使用它来代替成本高昂且局限的光纤通道或共享 SAS 电缆。

**存储总线层缓存。** 软件存储总线将存在的最快驱动器（例如 SSD）动态绑定到较慢的驱动器（例如 HDD），在服务器端提供读/写缓存，加速 IO 并提高吞吐量。

**存储池。** 形成存储空间基础的驱动器集合称为存储池。 存储池是自动创建的，它自动发现符合条件的所有驱动器，并将这些驱动器添加到池中。 强烈建议一个群集使用一个池，并采用默认设置。 请阅读我们的[深入探讨存储池](https://techcommunity.microsoft.com/t5/storage-at-microsoft/deep-dive-the-storage-pool-in-storage-spaces-direct/ba-p/425959)，了解详细信息。

**存储空间。** 存储空间使用[镜像和/或擦除编码](storage-spaces-fault-tolerance.md)为虚拟 "磁盘" 提供容错能力。 可以将其视为软件定义的分布式 RAID，使用的是池中的驱动器。 在存储空间直通中，除了机箱和机架容错外，这些虚拟磁盘通常还具有复原功能，可以复原两个同时发生的驱动器或服务器故障（例如，3 向镜像，各数据副本存储在不同的服务器中）。

**复原文件系统 (ReFS) 。** ReFS 是专门针对虚拟化构建的首要文件系统。 它可以显著加快 .vhdx 文件的操作速度（如创建、扩展以及检查点合并），并内置了校验和功能，可检测并纠正位错误。 它还引入了实时层，可以根据使用情况在所谓的“热”、“冷”存储层之间实时轮换数据。

**群集共享卷。** CSV 文件系统将所有 ReFS 卷整合为一个命名空间，可以通过任何服务器进行访问，对于每台服务器而言，每个卷的运行就像是本地安装在每台服务器上一样。

**横向扩展文件服务器。** 这是最后一层，仅在聚合部署中才需要。 它提供远程文件访问功能，可使用 SMB3 访问协议通过网络访问客户端（如运行 Hyper-V 的另一个群集），有效地将存储空间直通变为网络连接存储 (NAS)。

## <a name="customer-stories"></a>客户案例

全球有[超过10000群集](https://techcommunity.microsoft.com/t5/storage-at-microsoft/storage-spaces-direct-10-000-clusters-and-counting/ba-p/428185)运行存储空间直通。 各种规模的组织，从只部署两个节点的小型企业，到部署数百个节点的大型企业和政府，取决于其关键应用程序和基础结构的存储空间直通。

请访问[Microsoft.com/HCI](https://www.microsoft.com/hci)阅读其故事：

[![客户徽标网格](media/storage-spaces-direct-in-windows-server-2016/customer-stories.png)](https://www.microsoft.com/hci)

## <a name="management-tools"></a>管理工具

以下工具可用于管理和/或监视存储空间直通：

| 名称 | 图形或命令行？ | 支付还是包含？ |
|-----------------|----------------------------|-------------------|
| [Windows 管理中心](../../manage/windows-admin-center/overview.md)     | 图形    | Included |
| 服务器管理器 & 故障转移群集管理器                                 | 图形    | Included |
| Windows PowerShell                                                        | 命令行 | Included |
| [System Center Virtual Machine Manager (SCVMM) ](/system-center/vmm/s2d?view=sc-vmm-2019) <br>& [Operations Manager (SCOM) ](https://www.microsoft.com/download/details.aspx?id=54700) | 图形    | 已付     |

## <a name="get-started"></a>入门

[在 Microsoft Azure 中](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)试用存储空间直通，或者从 [Windows Server 评估](https://go.microsoft.com/fwlink/?linkid=842602) 中下载 Windows Server 的 180 天许可证评估副本。

## <a name="additional-references"></a>其他参考

- [容错和存储效率](storage-spaces-fault-tolerance.md)
- [存储副本](../storage-replica/storage-replica-overview.md)
- [Microsoft 博客上的存储](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)
- [具有 iWARP 的存储空间直通吞吐量](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)（TechNet 博客）
- [Windows Server 中的故障转移群集的新增功能](../../failover-clustering/whats-new-in-failover-clustering.md)
- [存储服务质量](../storage-qos/storage-qos-overview.md)
- [Windows IT 专业人员支持](https://www.microsoft.com/itpro/windows/support)
