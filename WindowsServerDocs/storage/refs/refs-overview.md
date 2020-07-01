---
title: 复原文件系统 (ReFS) 概述
ms.prod: windows-server
ms.author: gawatu
manager: mchad
ms.technology: storage-file-systems
ms.topic: article
author: gawatu
ms.date: 06/29/2019
ms.openlocfilehash: 5bcdbc76259d1dfecaaa5266bb952a21bcbc7825
ms.sourcegitcommit: 457e88e5aa6be13a2bffdb8e434a8efc3698678f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548892"
---
# <a name="resilient-file-system-refs-overview"></a>复原文件系统 (ReFS) 概述

>适用于： Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012，Windows Server （半年频道）

该复原文件系统 (ReFS) 是 Microsoft 的最新文件系统，可最大程度提升数据可用性、跨各种工作负载高效扩展到大数据集，并通过损坏复原提供数据完整性。 它旨在解决存储方案的扩展集问题以及为将来的革新打造基础。

## <a name="key-benefits"></a>主要优点

### <a name="resiliency"></a>复原

ReFS 引入了一项新功能，可以准确地检测到损坏并且还能够在保持联机状态的同时修复这些损坏，从而有助于增加你的数据的完整性和可用性：

- **完整性流** - ReFS 将校验和用于元数据和文件数据（可选），这使得 ReFS 能够可靠地检测到损坏。
- **存储空间集成** - 在与镜像或奇偶校验空间配合使用时，ReFS 可使用存储空间提供的备用数据副本自动修复检测到的损坏。 修复过程将本地化到损坏区域且联机执行，并且不会出现卷停机时间。
- **挽救数据** - 如果某个卷损坏并且损坏数据的备用副本不存在，则 ReFS 将从命名空间中删除损坏的数据。 ReFS 在处理大多数不可更正的损坏时可将卷保持在联机状态，但在极少数情况下，ReFS 需要将卷保持在脱机状态。
- **主动纠错** - 除了在读取和写入前对数据进行验证之外，ReFS 还引入了称为“清理器”的数据完整性扫描仪<i></i>。 此清理器会定期扫描卷，从而识别潜在损坏，然后主动触发损坏数据的修复。

### <a name="performance"></a>性能

除了提供复原能力改进之外，ReFS 还针对对性能极其敏感和虚拟化的工作负载引入新功能。 实时层优化、块克隆和稀疏 VDL 都是不断发展的 ReFS 功能的绝佳示例，它们专为支持各种动态工作负载而设计：

- **[镜像加速奇偶校验](./mirror-accelerated-parity.md)** - 镜像加速奇偶校验既可以提供高性能，也可为你的数据提供高效的容量存储。

    - 为了提供高性能和高效的容量存储，ReFS 会将卷划分为两个逻辑存储组，称为层。 这些层可具有自己的驱动器和复原类型，这使得能够针对性能或容量对每个层进行优化。 某些示例配置包括：

      | 性能层 | 容量层 |
      | ---------------- | ----------------- |
      | 镜像的 SSD | 镜像的 HDD |
      | 镜像的 SSD | 奇偶校验 SSD |
      | 镜像的 SSD | 奇偶校验 HDD |

    - 在配置了这些层后，ReFS 就会使用它们为热数据提供快速存储，以及为冷数据提供节省空间的存储：
        - 所有写入都将在性能层中发生，并且在性能层中保留的大数据区块将高效地实时移到容量层中。
        - 如果使用混合部署（混合使用闪存驱动器和 HDD 驱动器），[存储空间直通中的缓存](../storage-spaces/understand-the-cache.md)可帮助加快读取速度，从而降低虚拟化工作负荷的数据碎片特征的影响。 否则，如果使用的是双闪存部署，则读取也会出现在性能层中。

> [!NOTE]
> 对于服务器部署，镜像加速奇偶校验仅在[存储空间直通](../storage-spaces/storage-spaces-direct-overview.md)上受支持。 建议仅将镜像加速奇偶校验用于存档和备份工作负荷。 对于虚拟化和其他高性能随机工作负载，我们建议使用三向镜像以获得更好的性能。

- **加快 VM 操作** - ReFS 引入了为改善虚拟化工作负载的性能而专门设计的新功能：
    - [块克隆](./block-cloning.md) - 块克隆可加快复制操作的速度，并且能够实现快速、低影响的 VM 检查点合并操作。
    - 稀疏 VDL - 稀疏 VDL 允许 ReFS 将文件快速清零，从而将创建固定 VHD 所需的时间从几十分钟减少到仅仅几秒钟。

- **可变群集大小** - ReFS 支持 4K 和 64K 的群集大小。 4K 是针对大多数部署的建议的群集大小，但 64K 群集适合于大型的、顺序 IO 工作负载。

### <a name="scalability"></a>可伸缩性

ReFS 设计为支持非常大的数据集（数百万 TB 字节），而不会对性能有负面影响，并且与以前的文件相比实现了更好的扩展性。

## <a name="supported-deployments"></a>支持的部署

Microsoft 开发了 NTFS 专门用于广泛的配置和工作负荷，但对于特别需要 ReFS 提供的可用性、复原能力和/或规模的客户，Microsoft 支持在以下配置和方案下使用 ReFS。

> [!NOTE]
> 所有 ReFS 支持的配置必须使用[Windows Server 目录](https://www.WindowsServerCatalog.com)认证硬件，并满足应用程序要求。

### <a name="storage-spaces-direct"></a>存储空间直通

建议在存储空间直通上部署 ReFS，用于虚拟化工作负载或网络连接存储：
- 镜像加速奇偶校验和[存储空间直通中的缓存](../storage-spaces/understand-the-cache.md) 可提供高性能和高效的容量存储。
- 引入块克隆和稀疏 VDL 显著加快了创建、合并和扩展等 .vhdx 文件操作的速度。
- 完整性-流、联机修复和备用数据副本允许 ReFS 和存储空间直通共同检测和更正元数据和数据中的存储控制器和存储媒体损坏。
- ReFS 提供扩展和支持大量数据集的功能。

### <a name="storage-spaces"></a>存储空间

- 完整性流、联机修复和备用数据副本使 ReFS 和[存储空间](../storage-spaces/overview.md)可共同检测和更正元数据和数据中的存储控制器和存储媒体损坏。
- 存储空间部署还可以利用块克隆和 ReFS 中提供的可扩展性。
- 在带有共享 SAS 机箱的存储空间上部署 ReFS 适用于承载存档数据和存储用户文档。

> [!NOTE]
> 存储空间支持通过 BusTypes SATA、SAS 或 NVME 连接的本地非可移动直接连接，或者通过 HBA （亦即在直通模式下的 RAID 控制器）连接。

### <a name="basic-disks"></a>基本磁盘

在基本磁盘上部署 ReFS 最适用于实现其自己的软件复原能力和可用性解决方案的应用程序。
- 应用程序引入了自己的复原和可用性软件解决方案，可以利用完整性流、块克隆以及扩展和支持大量数据集的功能。

> [!NOTE]
> 基本磁盘包括通过 BusTypes SATA、SAS、NVME 或 RAID 的本地非可移动直接连接。 基本磁盘不包含存储空间。

### <a name="backup-target"></a>备份目标

将 ReFS 部署为备份目标最适用于实现其自己的复原能力和可用性解决方案的应用程序和硬件。
- 应用程序引入了自己的复原和可用性软件解决方案，可以利用完整性流、块克隆以及扩展和支持大量数据集的功能。

> [!NOTE]
> 备份目标包括上述受支持的配置。 请与应用程序和存储阵列供应商联系，以获取有关光纤通道和 iSCSI San 的支持详细信息。 对于 San，如果需要精简设置、剪裁/取消映射或卸载数据传输（ODX）等功能，则必须使用 NTFS。

## <a name="feature-comparison"></a>功能比较

### <a name="limits"></a>限制

| Feature       | ReFS                                        | NTFS |
|----------------|------------------------------------------------|-----------------------|
| 最大文件名称长度 | 255 个 Unicode 字符  | 255 个 Unicode 字符               |
| 最大路径名称长度 |32K Unicode 字符 | 32K Unicode 字符                |
| 文件大小上限 | 35 PB （pb）  | 256 TB               |
| 最大卷大小 | 35 PB                           | 256 TB                |

### <a name="functionality"></a>功能

#### <a name="the-following-features-are-available-on-refs-and-ntfs"></a>ReFS 和 NTFS 上提供以下功能：

| 功能       | ReFS                                        | NTFS |
|---------------------------|------------------|-----------------------|
| BitLocker 加密 | 是 | 是 |
| 重复数据删除 | 是<sup>1</sup> | 是 |
| 群集共享卷 (CSV) 支持 | Yes<sup>2</sup> | 是 |
| 软链接 | 是 | 是 |
| 故障转移群集支持 | 是 | 是 |
| 访问控制列表 | 是 | 是 |
| USN 日志 | 是 | 是 |
| 更改通知 | 是 | 是 |
| 交接点 | 是 | 是 |
| 装入点 | 是 | 是 |
| 重分析点 | 是 | 是 |
| 卷快照 | 是 | 是 |
| 文件 ID | 是 | 是 |
| Oplocks | 是 | 是 |
| 稀疏文件 | 是 | 是 |
| 命名流 | 是 | 是 |
| 精简预配 | 是<sup>3</sup> | 是 |
| 剪裁/取消映射 | 是<sup>3</sup> | 是 |
1. 在 Windows Server 版本1709及更高版本上可用。
2. 在 Windows Server 2012 R2 及更高版本上可用。
3. 仅存储空间

#### <a name="the-following-features-are-only-available-on-refs"></a>ReFS 上仅提供以下功能：

| 功能       | ReFS                                        | NTFS |
|---------------------------|------------------|-----------------------|
| 块克隆 | 是 | 否 |
| 稀疏 VDL | 是 | 否 |
| 镜像加速奇偶校验| 是（在存储空间直通上） | 否 |

#### <a name="the-following-features-are-unavailable-on-refs-at-this-time"></a>目前 ReFS 上未提供以下功能：

| 功能       | ReFS                                        | NTFS |
|---------------------------|------------------|-----------------------|
| 文件系统压缩 | 否 | 是 |
| 文件系统加密 | 否 | 是 |
| 事务 | 否 | 是 |
| 硬链接 | 否 | 是 |
| 对象 ID | 否 | 是 |
| 卸载数据传输（ODX） | 否 | 是 |
| 短名称 | 否 | 是 |
| 扩展的属性 | 否 | 是 |
| 磁盘配额 | 否 | 是 |
| 可引导 | 否 | 是 |
| 页面文件支持 | 否 | 是 |
| 在可移动媒体上受支持 | 否 | 是 |

## <a name="additional-references"></a>其他参考

- [ReFS 和 NTFS 的群集大小建议](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [存储空间直通概述](../storage-spaces/storage-spaces-direct-overview.md)
- [ReFS 块克隆](block-cloning.md)
- [ReFS 完整性流](integrity-streams.md)
- [通过 ReFSUtil 排查 ReFS 问题](../../administration/windows-commands/refsutil.md)
