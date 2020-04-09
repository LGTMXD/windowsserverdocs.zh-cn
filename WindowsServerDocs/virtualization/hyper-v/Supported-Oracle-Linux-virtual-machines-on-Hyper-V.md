---
title: Hyper-v 上支持的 Oracle Linux 虚拟机
description: 列出每个版本中包含的 Linux integration services 和功能
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: c02fdb5b-62f3-43cb-a190-ab74b3ebcf77
author: shirgall
ms.author: kathydav
ms.date: 06/01/2017
ms.openlocfilehash: edf92689f1dbe93c387c65e64694c64635fe3958
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858010"
---
# <a name="supported-oracle-linux-virtual-machines-on-hyper-v"></a>Hyper-v 上支持的 Oracle Linux 虚拟机

>适用于： Windows Server 2019，Windows Server 2016，Hyper-v Server 2016，Windows Server 2012 R2，Hyper-v server 2012 R2，Windows Server 2012，Hyper-v Server 2012，Windows Server 2008 R2，Windows 10，Windows 8.1，Windows 8，Windows 7.1，Windows 7

以下功能分发映射指示每个版本中的功能。 表后面列出了每个分发的已知问题和解决方法。

本节内容：

* [与 Red Hat 兼容内核 Oracle Linux 版本的功能](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_rhc)

* [Oracle Linux 版本与 Unbreakable Enterprise 内核（UEK）](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_uek)

* [注意](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_notes)

## <a name="table-legend"></a>表图例

* **内置**的-.lis 作为此 Linux 分发的一部分包含在内。 内置 .LIS 的内核模块版本号（如**lsmod**所示）不同于 Microsoft 提供的 .lis 下载包中的版本号。 不匹配并不表明内置的 .LIS 版本已过期。

* &#10004;-可用功能

* （*空白*）-功能不可用

* **UEK RxUy** -Unbreakable Enterprise KERNEL （UEK），其中 x 是版本号，y 是季度更新。

## <a name="features-of-oracle-linux-releases-with-the-red-hat-compatible-kernel"></a><a name="BKMK_rhc"></a>与 Red Hat 兼容内核 Oracle Linux 版本的功能

用于1.x 系列的32位内核启用了 PAE。 Oracle Linux RHCK 6.0-6.3 的内置 .LIS 支持。 Oracle Linux 7. x 内核仅限64位。

| **具有**                                                                                                                                  | **Windows server 版本**         | **7.5-7。6**        | **7.4**             | **6.4-6.8 和 7.0-7。3**                                             | **6.4-6.8 和 7.0-7。2**                                             | **带有 RHCK 7.0-7.2 的 OL**         | **RHCK 6.8 的 OL**             | **带 RHCK 6.6 的 OL，6。7**        | **RHCK 6.5 的 OL**              | **带有 RHCK 6.4 的 OL**               |
|----------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|--------------------|---------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|--------------------------|--------------------------|--------------------------|---------------------------|---------------------------|
| **可用性**                                                                                                                             |                                    | 内置           | 内置            | [.LIS 4。2](https://www.microsoft.com/download/details.aspx?id=55106) | [.LIS 4。1](https://www.microsoft.com/download/details.aspx?id=51612) | 内置                 | 内置                 | 内置                 | 内置                  | 内置                  |
| **[转储](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                                                   | 2019、2016、2012 R2、2012、2008 R2 | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| Windows Server 2016 准确时间                                                                                                            | 2019、2016                         |                    |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[上网](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                                       |                                    |                    |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Jumbo 帧                                                                                                                                 | 2019、2016、2012 R2、2012、2008 R2 | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| VLAN 标记和中继                                                                                                                    | 2019、2016、2012 R2、2012、2008 R2 | &#10004;           | &#10004;            | &#10004;（备注1表示 6.4-6.8）                                       | &#10004;（备注1表示 6.4-6.8）                                       | &#10004;                 | &#10004;备注1          | &#10004;备注1          | &#10004;备注1           | &#10004;备注1           |
| 实时迁移                                                                                                                               | 2019、2016、2012 R2、2012、2008 R2 | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| 静态 IP 注入                                                                                                                          | 2019、2016、2012 R2、2012          | &#10004;备注14   | &#10004;备注14    | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| vRSS                                                                                                                                         | 2019、2016、2012 R2                | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 |                           |                           |
| TCP 分段和校验和卸载                                                                                                       | 2019、2016、2012 R2、2012、2008 R2 | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 |                           |                           |
| SR-IOV                                                                                                                                       | 2019、2016                         | &#10004;           | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[储存](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                                             |                                    |                    |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| VHDX 调整大小                                                                                                                                  | 2019、2016、2012 R2                | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| 虚拟光纤通道                                                                                                                        | 2019、2016、2012 R2                | &#10004;备注2    | &#10004;备注2     | &#10004;备注2                                                     | &#10004;备注2                                                     | &#10004;备注2          | &#10004;备注2          | &#10004;备注2          | &#10004;备注2           |                           |
| 实时虚拟机备份                                                                                                                  | 2019、2016、2012 R2                | &#10004;注释11、3 | &#10004;注释11、3 | &#10004;备注3，4                                                  | &#10004;备注3，4                                                  | &#10004;备注3、4、11   | &#10004;备注3、4、11   | &#10004;备注3、4、11   | &#10004;备注3、4、5、11 | &#10004;备注3、4、5、11 |
| 剪裁支持                                                                                                                                 | 2019、2016、2012 R2                | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 |                          |                           |                           |
| SCSI WWN                                                                                                                                     | 2019、2016、2012 R2                | &#10004;           |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| **[记忆](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                                               |                                    |                    |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| PAE 内核支持                                                                                                                           | 2019、2016、2012 R2、2012、2008 R2 | 不可用                | 不可用                 | &#10004;（仅限1.x）                                                 | &#10004;（仅限1.x）                                                 | 不可用                      | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| MMIO 间隙的配置                                                                                                                    | 2019、2016、2012 R2                | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| 动态内存-热添加                                                                                                                     | 2019、2016、2012 R2、2012          | &#10004;备注8、9 | &#10004;备注8、9  | &#10004;备注7、8、9、10（备注6适用于 6.4-6.7）                      | &#10004;备注7、8、9、10（备注6适用于 6.4-6.7）                      | &#10004;备注6、7、8、9 | &#10004;备注6、7、8、9 | &#10004;备注6、7、8、9 | &#10004;备注6、7、8、9  |                           |
| 动态内存-膨胀                                                                                                                  | 2019、2016、2012 R2、2012          | &#10004;备注8、9 | &#10004;备注8、9  | &#10004;备注7、9、10（备注6适用于 6.4-6.7）                         | &#10004;备注7、9、10（备注6适用于 6.4-6.7）                         | &#10004;备注6、8、9    | &#10004;备注6、8、9    | &#10004;备注6、8、9    | &#10004;备注6、8、9     | &#10004;备注6、8、9、10 |
| 运行时内存大小调整                                                                                                                        | 2019、2016                         |                    |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[显示](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                                                 |                                    |                    |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Hyper-v 特定视频设备                                                                                                                | 2019、2016、2012 R2、2012、2008 R2  | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| **[杂](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                                 |                                    |                    |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| 键值对                                                                                                                               | 2019、2016、2012 R2、2012、2008 R2 | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;备注12         | &#10004;备注12         | &#10004;备注12         | &#10004;备注12          | &#10004;备注12          |
| 不可屏蔽中断                                                                                                                       | 2019、2016、2012 R2                | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| 从主机到来宾的文件复制                                                                                                                 | 2019、2016、2012 R2                | &#10004;           | &#10004;            | &#10004;                                                            | &#10004;                                                            |                          | &#10004;                 |                          |                           |                           |
| lsvmbus 命令                                                                                                                              | 2019、2016、2012 R2、2012、2008 R2 |                    |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| Hyper-v 套接字                                                                                                                              | 2019、2016                         |                    |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| PCI 传递/DDA                                                                                                                          | 2019、2016                         | &#10004;           | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[第2代虚拟机](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                    |                    |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| 使用 UEFI 启动                                                                                                                              | 2019、2016、2012 R2                | &#10004;备注13   | &#10004;备注13    | &#10004;备注13                                                    | &#10004;备注13                                                    | &#10004;备注13         | &#10004;备注13         |                          |                           |                           |
| 安全启动                                                                                                                                  | 2019、2016                         | &#10004;           | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |


## <a name="oracle-linux-releases-with-the-unbreakable-enterprise-kernel-uek"></a><a name="BKMK_uek"></a>Oracle Linux 版本与 Unbreakable Enterprise 内核（UEK）

Unbreakable Enterprise 内核（UEK） Oracle Linux 仅限64位，并内置了 IIS 内置支持。 

| **具有**                                                                                                                                  | **Windows server 版本**         | **R5**                | **R4**                | **R3 QU3**            | **R3 QU2**            | **R3 QU1**       |
|----------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|---------------------------|---------------------------|---------------------------|---------------------------|----------------------|
| **可用性**                                                                                                                             |                                    | 内置                  | 内置                  | 内置                  | 内置                  | 内置             |
| **[转储](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                                                   | 2019、2016、2012 R2、2012、2008 R2 | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;             |
| Windows Server 2016 准确时间                                                                                                            | 2019、2016                         |                           |                           |                           |                           |                      |
| **[上网](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                                       |                                    |                           |                           |                           |                           |                      |
| Jumbo 帧                                                                                                                                 | 2019、2016、2012 R2、2012、2008 R2 | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;             |
| VLAN 标记和中继                                                                                                                    | 2019、2016、2012 R2、2012、2008 R2 | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;             |
| 实时迁移                                                                                                                               | 2019、2016、2012 R2、2012、2008 R2 | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;             |
| 静态 IP 注入                                                                                                                          | 2019、2016、2012 R2、2012          | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  |                      |
| vRSS                                                                                                                                         | 2019、2016、2012 R2                | &#10004;                  | &#10004;                  |                           |                           |                      |
| TCP 分段和校验和卸载                                                                                                       | 2019、2016、2012 R2、2012、2008 R2 | &#10004;                  | &#10004;                  |                           |                           |                      |
| SR-IOV                                                                                                                                       | 2019、2016                         |                           |                           |                           |                           |                      |
| **[储存](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                                             |                                    |                           |                           |                           |                           |                      |
| VHDX 调整大小                                                                                                                                  | 2019、2016、2012 R2                | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  |                      |
| 虚拟光纤通道                                                                                                                        | 2019、2016、2012 R2                | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  |                      |
| 实时虚拟机备份                                                                                                                  | 2019、2016、2012 R2                | &#10004;备注3、4、5、11 | &#10004;备注3、4、5、11 | &#10004;备注3、4、5、11 | &#10004;备注3、4、5、11 |                      |
| 剪裁支持                                                                                                                                 | 2019、2016、2012 R2                | &#10004;                  | &#10004;                  |                           |                           |                      |
| SCSI WWN                                                                                                                                     | 2019、2016、2012 R2                |                           |                           |                           |                           |                      |
| **[记忆](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                                               |                                    |                           |                           |                           |                           |                      |
| PAE 内核支持                                                                                                                           | 2019、2016、2012 R2、2012、2008 R2 | 不可用                       | 不可用                       | 不可用                       | 不可用                       | 不可用                  |
| MMIO 间隙的配置                                                                                                                    | 2019、2016、2012 R2                | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;             |
| 动态内存-热添加                                                                                                                     | 2019、2016、2012 R2、2012          | &#10004;                  | &#10004;                  |                           |                           |                      |
| 动态内存-膨胀                                                                                                                  | 2019、2016、2012 R2、2012          | &#10004;                  | &#10004;                  |                           |                           |                      |
| 运行时内存大小调整                                                                                                                        | 2019、2016                         |                           |                           |                           |                           |                      |
| **[显示](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                                                 |                                    |                           |                           |                           |                           |                      |
| Hyper-v 特定视频设备                                                                                                                | 2019、2016、2012 R2、2012、2008 R2 | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  |                      |
| **[杂](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                                 |                                    |                           |                           |                           |                           |                      |
| 键值对                                                                                                                               | 2019、2016、2012 R2、2012、2008 R2 | &#10004;注释11、12      | &#10004;注释11、12      | &#10004;注释11、12      | &#10004;注释11、12      | &#10004;注释11、12 |
| 不可屏蔽中断                                                                                                                       | 2019、2016、2012 R2                | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;                  | &#10004;             |
| 从主机到来宾的文件复制                                                                                                                 | 2019、2016、2012 R2                | &#10004;注释11          | &#10004;注释11          | &#10004;注释11          | &#10004;注释11          | &#10004;注释11     |
| lsvmbus 命令                                                                                                                              | 2019、2016、2012 R2、2012、2008 R2 |                           |                           |                           |                           |                      |
| Hyper-v 套接字                                                                                                                              | 2019、2016                         |                           |                           |                           |                           |                      |
| PCI 传递/DDA                                                                                                                          | 2019、2016                         |                           |                           |                           |                           |                      |
| **[第2代虚拟机](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                    |                           |                           |                           |                           |                      |
| 使用 UEFI 启动                                                                                                                              | 2019、2016、2012 R2                | &#10004;                  | &#10004;                  |                           |                           |                      |
| 安全启动                                                                                                                                  | 2019、2016                         | &#10004;                  | &#10004;                  |                           |                           |                      |

## <a name="notes"></a><a name="BKMK_notes"></a>本票

1. 对于此 Oracle Linux 版本，VLAN 标记有效，但 VLAN 中继不起作用。

2. 使用虚拟光纤通道设备时，请确保已填充逻辑单元号0（LUN 0）。 如果尚未填充 LUN 0，Linux 虚拟机可能无法以本机方式装载光纤通道设备。

3. 如果在执行实时虚拟机备份操作的过程中有打开的文件句柄，则在某些角落情况下，备份的 Vhd 可能需要在还原时执行文件系统一致性检查（fsck）。

4. 如果虚拟机有连接的 iSCSI 设备或直接连接的存储（也称为传递磁盘），则实时备份操作可能会悄悄地失败。

5. 使用 UEK R3Q2 和 UEK R3Q3 的实时备份支持 Oracle Linux 6 更新4和 Oracle Linux 6 Update 5 可通过[适用于 Linux 的 Hyper-v Backup Essentials](https://github.com/LIS/backupessentials/tree/1.0)获得。

6. 动态内存支持仅适用于64位虚拟机。

7. 默认情况下，此分发中未启用热添加支持。 若要启用热添加支持，需要在/etc/udev/rules.d/下添加 udev 规则，如下所示：

   1. 创建文件 **/etc/udev/rules.d/100-balloon.rules**。 您可以为该文件使用任何其他所需的名称。

   2. 将以下内容添加到文件中： `SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. 重新启动系统以启用热添加支持。

   尽管 Linux Integration Services 下载会在安装时创建此规则，但卸载 .LIS 时也会删除该规则，因此，如果在卸载之后需要动态内存，则必须重新创建该规则。

8. 如果来宾操作系统在内存上运行得太低，动态内存操作可能会失败。 下面是一些最佳做法：

   * 启动内存和最小内存应等于或大于分发供应商建议的内存量。

   * 通常会消耗系统中的全部可用内存的应用程序，仅消耗最多80% 的可用 RAM。

9. 如果在 Windows Server 2016 或 Windows Server 2012 R2 操作系统上使用动态内存，请以128兆字节（MB）为单位指定 "**启动内存**"、"**最小内存**" 和 "**最大内存**" 参数。 如果不这样做，可能会导致热添加失败，并且在来宾操作系统中可能看不到任何内存增长。

10. 某些分发版（包括使用 .LIS 3.5 或 .LIS 4.0 的发行版）仅提供膨胀支持，不提供热添加支持。 在这种情况下，可以通过将 "启动内存" 参数设置为与 "最大内存" 参数相等的值来使用动态内存功能。 这会导致在启动时将所有必要的内存热添加到虚拟机，然后根据主机的内存要求，Hyper-v 可以使用膨胀从来宾自由分配或释放内存。 请在或更高版本的推荐值上配置**启动内存**和**最小内存**。

11. 默认情况下，不会安装 Oracle Linux Hyper-v 守护程序。 若要使用这些守护程序，请安装 hyperv 守护程序包。 此包与下载的 Linux Integration Services 冲突，不应安装在下载了 .LIS 的系统上。

12. 如果没有 Linux 软件更新，键/值对（KVP）基础结构可能无法正常运行。 请与您的分销商联系以获取软件更新，以防您看到此功能的问题。

13. 依赖 Server 2012 R2Generation 2 虚拟机默认已启用安全启动，某些 Linux 虚拟机将无法启动，除非禁用了安全启动选项。 你可以在**Hyper-v 管理器**中虚拟机设置的 "**固件**" 部分禁用安全启动，也可以使用 Powershell 禁用它：

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    可以将 Linux Integration Services 下载应用到现有的第2代 Vm，但不授予第2代功能。

14. 如果为虚拟机上的指定合成网络适配器配置了网络管理器，则静态 IP 注入可能不起作用。 要使静态 IP 注入正常运行，请确保已完全关闭网络管理器，或已通过 ifcfg-eth0-ethX 文件为特定网络适配器关闭网络管理器。


另请参阅

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Hyper-v 上支持的 CentOS 和 Red Hat Enterprise Linux 虚拟机](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-V 上支持的 Debian 虚拟机](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上支持的 SUSE 虚拟机](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上支持的 Ubuntu 虚拟机](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上支持的 FreeBSD 虚拟机](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上的 Linux 和 FreeBSD 虚拟机的功能说明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [在 Hyper-v 上运行 Linux 的最佳实践](Best-Practices-for-running-Linux-on-Hyper-V.md)
