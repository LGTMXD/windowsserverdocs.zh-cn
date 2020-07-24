---
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
title: 选择存储空间直通驱动器
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: bdd5264394c94748b7720842cf8ff7e01e1375e7
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965419"
---
# <a name="choosing-drives-for-storage-spaces-direct"></a>选择存储空间直通驱动器

>适用于：Windows Server 2019、Windows Server 2016

本主题提供有关如何选择[存储空间直通](storage-spaces-direct-overview.md)驱动器以满足你的性能和容量要求的指南。

## <a name="drive-types"></a>驱动器类型

存储空间直通当前适用于四种类型的驱动器：

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/pmem-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>PMem</b>指持久性内存，一种新的低延迟、高性能存储类型。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>NVMe</b>（非易失性内存 Express）指的是直接位于 PCIe 总线上的固态硬盘。 常见的外形规格是 2.5 英寸 U.2、PCIe 外接卡 (AIC) 和 M.2。 NVMe 提供更高的 IOPS 和 IO 吞吐量，延迟时间比我们目前支持的任何其他类型的驱动器（持久性内存除外）的延迟更高。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px" >
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>SSD</b> 指的是通过传统 SATA 或 SAS 进行连接的固态硬盘。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>HDD</b> 指的是提供大量存储容量的旋转式磁性硬盘驱动器。
        </td>
    </tr>
</table>

## <a name="built-in-cache"></a>内置缓存

存储空间直通具有内置服务器端缓存。 这是一个大型、持久且实时的读取和写入缓存。 在部署多种类型的驱动器时，它会被自动配置为使用所有“最快”类型的驱动器。 剩余的驱动器用于提供容量。

有关详细信息，请查看[了解存储空间直通中的缓存](understand-the-cache.md)。

## <a name="option-1--maximizing-performance"></a>选项 1 - 最大程度地提高性能

若要实现对任何数据的随机读取和写入的可预测且统一的亚毫秒级延迟，或者要实现极高的 IOPS（我们已实现了[超过六百万](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m)！）或 IO 吞吐量（我们已实现了[超过 1 Tb/s](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s)！），那么你应该选择“全闪存”。

为此，目前有三种方法：

![All-Flash-Deployment-Possibilities](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **所有 NVMe。** 使用所有 NVMe 会提供无与伦比的性能，包括具有最高可预测性的低延迟。 如果你的所有驱动器都具有相同型号，则没有缓存。 你还可以混用高耐用性和低耐用性的 NVMe 型号，并且将前者配置为缓存对后者的写入（[需要设置](understand-the-cache.md#manual-configuration)）。

2. **NVMe + SSD。** 通过将 NVMe 与 SSD 一起使用，NVMe 将自动缓存对 SSD 的写入。 这允许写入缓存中的合并，并且仅在需要时取消暂存，从而降低了 SSD 上的磨损。 这提供与 NVMe 类似的写入特性，同时支持直接从速度同样快的 SSD 上进行读取。

3. **所有 SSD。** 与全 NVMe 一样，如果你的所有驱动器均为相同型号，则没有缓存。 如果你混用更高耐用性和更低耐用性的型号，则可以将前者配置为缓存对后者的写入（[要求设置](understand-the-cache.md#manual-configuration)）。

   >[!NOTE]
   > 在没有缓存的情况下使用全 NVMe 或全 SSD 的好处在于，你可以从每个驱动器获取有用的存储容量。 没有对于缓存的容量“消耗”，这在较小的规模上可能很有吸引力。

## <a name="option-2--balancing-performance-and-capacity"></a>选项 2 - 在性能和容量之间实现平衡

对于具有多种不同应用程序和工作负载的环境（有些具有严格的性能要求，其他需要相当高的存储容量），你应该针对较大的 HDD 选择具有 NVMe 或 SSD 缓存的“混合”结构。

![Hybrid-Deployment-Possibilities](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe + HDD**。 NVMe 驱动器通过对读写操作进行缓存，加快读取和写入的速度。 通过对读取进行缓存，可以让 HDD 把重心放在写入上。 通过对写入进行缓存，可以采用让 HDD IOPS 和 IO 吞吐量最大化的人为串行化方式，吸收突发流量并使写入在仅需要时合并和取消暂存。 这提供与 NVMe 类似的写入特性，并且对于常用数据或者最近读取的数据，还提供与 NVMe 类似的读取特性。

2. **SSD + HDD**。 如上所述，SSD 可通过对读写操作进行缓存，加快读取和写入的速度。 这提供与 SSD 类似的写入特性，并且对于经常读取数据或最近读取数据，还提供与 SSD 类似的读取特性。

    还有一个很不寻常的附加选项：使用*全部三种*类型的驱动器。

3. **NVMe + SSD + HDD。** 如果有所有三种类型的驱动器，NVMe 驱动器会对 SSD 和 HDD 进行缓存。 有吸引力的地方在于，你可以在 SSD 上创建卷以及在 HDD 上创建卷，它们并行位于同一个群集中，并且全都由 NVMe 分配。 前者就像是在“全闪存”部署环境中，而后者就像是在上文所述的“混合”部署环境中。 这在概念上类似具有两个池，主要采用独立的容量管理以及失败和维修周期等。

   >[!IMPORTANT]
   > 我们建议使用 SSD 层将对性能最敏感的工作负载放在全闪存中。

## <a name="option-3--maximizing-capacity"></a>选项 3 - 最大程度地提高容量

对于不经常需要大量容量和写入的工作负载，例如存档、备份目标、数据仓库或“冷”存储，你应该将用于缓存的少量 SSD 与用于容量的许多较大的 HDD 结合在一起。

![用于最大程度地提高容量的部署选项](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSD + HDD**。 这些 SSD 将缓存读取和写入、吸收突发流量并且提供类似 SSD 的写入性能，方法是稍后针对 HDD 提供优化的取消暂存。

>[!IMPORTANT]
>仅支持带有 Hdd 的配置。 不建议将高耐用性 Ssd 缓存到低耐用性 Ssd。

## <a name="sizing-considerations"></a>调整大小注意事项

### <a name="cache"></a>缓存

每个服务器都必须具有至少两个缓存驱动器（针对冗余的最低要求）。 我们建议容量驱动器数量是缓存驱动器数量的倍数。 例如，如果你有 4 个缓存驱动器，则使用 8 个容量驱动器（1:2 的比率），这样一来，你所能体验到的性能将比使用 7 个或 9 个容量驱动器更一致。

应该调整缓存的大小，以适应应用程序和工作负荷的工作集，即，在任何给定时间，它们正在主动读取和写入的所有数据。 没有除此之外的缓存大小要求。 对于使用 Hdd 的部署，一个合理的起点是容量的10% –例如，如果每个服务器具有 4 x 4 TB HDD = 16 TB 的容量，则 2 x 800 GB SSD = 1.6 TB 的缓存每个服务器。 对于所有闪存部署，尤其是对于非常[高](https://techcommunity.microsoft.com/t5/storage-at-microsoft/understanding-ssd-endurance-drive-writes-per-day-dwpd-terabytes/ba-p/426024)的 ssd，尤其是在容量非常高的情况下（例如，如果每台服务器具有 24 x 1.2 TB SSD = 28.8 TB 的容量），则 2 x 750 GB NVMe = 每个服务器的缓存 1.5 tb。 你始终可以在以后添加或移除缓存驱动器来进行调整。

### <a name="general"></a>常规

建议将每个服务器的总存储容量限制为约 400 tb。 每个服务器的存储容量越高，在停机或重启后重新同步数据所需的时间就越长，例如在应用软件更新时。 对于 Windows Server 2019，每个存储池的当前最大大小为 4 pb （PB）（4000 TB），对于 Windows Server 2016 为 1 pb。

## <a name="additional-references"></a>其他参考

- [存储空间直通概述](storage-spaces-direct-overview.md)
- [了解存储空间直通中的缓存](understand-the-cache.md)
- [存储空间直通硬件要求](storage-spaces-direct-hardware-requirements.md)
- [在存储空间直通中规划卷](plan-volumes.md)
- [容错和存储效率](storage-spaces-fault-tolerance.md)
