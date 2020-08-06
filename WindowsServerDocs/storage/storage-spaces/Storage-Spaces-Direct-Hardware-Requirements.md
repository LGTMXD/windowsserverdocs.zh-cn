---
title: 存储空间直通硬件要求
ms.prod: windows-server
description: 测试存储空间直通的最低硬件要求。
ms.author: eldenc
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 07/24/2020
ms.localizationpriority: medium
ms.openlocfilehash: 45ef438d58c9d36275f2e7a32ce93a383bd21a70
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864272"
---
# <a name="storage-spaces-direct-hardware-requirements"></a>存储空间直通的硬件要求

> 适用于：Windows Server 2019、Windows Server 2016

本主题描述 Windows Server 上存储空间直通的最低硬件要求。 对于 Azure Stack HCI 上的硬件要求，为通过与云连接而设计的超聚合部署的操作系统，请参阅[部署 Azure Stack HCI 之前，请参阅部署 HCI：确定硬件要求](/azure-stack/hci/deploy/before-you-start#determine-hardware-requirements)。

对于生产环境，Microsoft 建议购买合作伙伴提供的经验证的硬件/软件解决方案，其中包括部署工具和过程。 针对我们的参考体系结构设计、汇编和验证这些解决方案，以确保兼容性和可靠性，使你能够快速启动和运行。 对于 Windows Server 2019 解决方案，请访问[AZURE STACK HCI 解决方案网站](https://azure.microsoft.com/overview/azure-stack/hci)。 对于 Windows Server 2016 解决方案，请参阅[Windows Server 软件定义](https://microsoft.com/wssd)的详细信息。

   > [!TIP]
   > 想要评估存储空间直通但没有硬件？ 使用[来宾虚拟机群集中的存储空间直通中](storage-spaces-direct-in-vm.md)所述的 Hyper-v 或 Azure 虚拟机。

## <a name="base-requirements"></a>基本要求

系统、组件、设备和驱动程序必须是按照[Windows Server 目录](https://www.windowsservercatalog.com)**认证的 windows server 2016** 。 此外，我们建议服务器、驱动器、主机总线适配器和网络适配器都具有**软件定义的数据中心 (sddc) 标准**和/或**软件定义的数据中心 (sddc) 高级**额外资格 (AQs) ，如下图所示。 具有 SDDC AQs 的组件超过1000个。

![显示 SDDC AQs 的 Windows Server 目录的屏幕截图](media/hardware-requirements/sddc-aqs.png)

完全配置的群集 (服务器、网络和存储) 必须通过向导中的每个向导或故障转移群集管理器在 PowerShell 中通过 cmdlet 传递所有[群集验证测试](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732035(v=ws.10)) `Test-Cluster` [cmdlet](/powershell/module/failoverclusters/test-cluster?view=win10-ps) 。

此外，还需要满足以下要求：

## <a name="servers"></a>服务器

- 最少 2 台服务器，最多 16 台服务器
- 建议所有服务器都是相同的制造商和型号

## <a name="cpu"></a>CPU

- Intel Nehalem 或更高版本的兼容处理器;或
- AMD EPYC 或更高版本的兼容处理器

## <a name="memory"></a>内存

- 适用于 Windows Server、Vm 和其他应用或工作负荷的内存;加大
- 每 tb 每 tb (TB) 缓存驱动器容量的 RAM，适用于存储空间直通元数据

## <a name="boot"></a>启动

- Windows Server 支持的任何启动设备，[现在包括 SATADOM](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/)
- RAID 1 镜像**不**是必需的，但支持启动
- 建议： 200 GB 的最小大小

## <a name="networking"></a>网络

存储空间直通需要在每个节点之间进行可靠的高带宽、低延迟的网络连接。  

小规模2-3 节点的最小互连
- 10 Gbps 网络接口卡 (NIC) 或更快
- 每个节点中有两个或更多个网络连接，以实现冗余和性能

适用于高性能、大规模或部署 4 + 的建议互连 
- 远程直接内存访问 (RDMA) 支持的 Nic、iWARP (建议的) 或 RoCE
- 每个节点中有两个或更多个网络连接，以实现冗余和性能
- 25 Gbps NIC 或更快

交换或 switchless 节点互连
- 交换：必须正确配置网络交换机以处理带宽和网络类型。  如果使用的 RDMA 实现了 RoCE 协议，则网络设备和交换机配置更为重要。 
- Switchless：可以使用直接连接互连节点，避免使用交换机。  每个节点都必须与群集中的每个其他节点具有直接连接。


## <a name="drives"></a>驱动器

存储空间直通使用直接连接 SATA、SAS、NVMe 或永久性内存 (PMem) 驱动器，每个驱动器都物理连接到一台服务器。 有关选择驱动器的更多帮助，请参阅[选择驱动器](choosing-drives.md)和[理解和部署永久性内存](deploy-pmem.md)主题。

- 支持 SATA、SAS、永久性内存和 NVMe (2、U. 2 和外接程序卡) 驱动器。
- 支持512n、512e 和4K 本机驱动器
- 固态硬盘必须提供[电源丢失保护](https://techcommunity.microsoft.com/t5/storage-at-microsoft/don-t-do-it-consumer-grade-solid-state-drives-ssd-in-storage/ba-p/425914)
- 每个服务器中相同数量和类型的驱动器–请参阅[驱动对称注意事项](drive-symmetry-considerations.md)
- 缓存设备必须为 32 GB 或更大
- 永久性内存设备在块存储模式下使用
- 当使用永久性内存设备作为缓存设备时，必须使用 NVMe 或 SSD 容量设备， (不能使用 Hdd) 
- NVMe 驱动程序是 Microsoft 提供的驱动程序，它包含在 Windows ( # A0) 
- 建议：容量驱动器数是缓存驱动器数的整数倍
- 建议：缓存驱动器应具有高写入高耐用性：每日至少3个驱动器写入 (DWPD) 或至少 4 tb 写入 (TBW) ，请参阅[了解每日的驱动器写入数 (DWPD) ，tb 写入 (TBW) ，以及建议的最小值存储空间直通](https://techcommunity.microsoft.com/t5/storage-at-microsoft/understanding-ssd-endurance-drive-writes-per-day-dwpd-terabytes/ba-p/426024)

下面是如何连接存储空间直通的驱动器：

- 直连 SATA 驱动器
- 直连 NVMe 驱动器
- SAS 主机总线适配器 (HBA) 与 SAS 驱动器
- SAS 主机总线适配器 (HBA) 与 SATA 驱动器
- **不支持：** RAID 控制器卡或 SAN (光纤通道、iSCSI、FCoE) 存储。 主机总线适配器 (HBA) 卡必须实现简单的传递模式。

![受支持的驱动器互连示意图](media/hardware-requirements/drive-interconnect-support-1.png)

驱动器可以是服务器的内部，也可以是仅连接到一台服务器的外部存储设备。 槽映射和标识需要 SCSI 机箱服务 (SES) 。 每个外部机箱必须提供唯一标识符 (唯一 ID) 。

- 服务器的内部驱动器
- 外部机箱中的驱动器 ( "JBOD" ) 连接到一台服务器
- **不支持：** 共享 SAS 机箱连接到多台服务器或任何形式的多路径 IO (MPIO) ，驱动器可通过多个路径进行访问。

![受支持的驱动器互连示意图](media/hardware-requirements/drive-interconnect-support-2.png)

### <a name="minimum-number-of-drives-excludes-boot-drive"></a>驱动器的最小数目 (排除启动驱动器) 

- 如果有用作缓存的驱动器，则每个服务器必须至少有 2 个驱动器
- 每个服务器必须至少有 4 个容量（非缓存）驱动器

| 存在驱动器类型   | 所需的最小数量 |
|-----------------------|-------------------------|
| 所有永久内存 (相同的模型)  | 4永久性内存 |
| 所有 NVMe（同一型号） | 4 个 NVMe                  |
| 所有 SSD（同一型号）  | 4 个 SSD                   |
| 永久性内存 + NVMe 或 SSD | 2永久性内存 + 4 NVMe 或 SSD |
| NVMe + SSD            | 2 个 NVMe + 4 个 SSD          |
| NVMe + HDD            | 2 个 NVMe + 4 个 HDD          |
| SSD + HDD             | 2 个 SSD + 4 个 HDD           |
| NVMe + SSD + HDD      | 2 个 NVMe + 4 个其他       |

   >[!NOTE]
   > 此表提供了硬件部署的最低要求。 如果要使用虚拟机和虚拟化存储（如 Microsoft Azure 中的存储）进行部署，请参阅在[来宾虚拟机群集中使用存储空间直通](storage-spaces-direct-in-vm.md)。

### <a name="maximum-capacity"></a>最大容量

| 最                | Windows Server 2019  | Windows Server 2016  |
| ---                     | ---------            | ---------            |
| 每台服务器的原始容量 | 400 TB               | 100 TB               |
| 池容量           | 4 PB (4000 TB)       | 1 PB                 |
