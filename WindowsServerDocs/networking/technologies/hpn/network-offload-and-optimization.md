---
title: 网络卸载和优化技术
description: 本主题概述 Windows Server 2016 中的卸载和优化技术，并提供指向有关这些技术的其他指南的链接。
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: e6f53fa8462a51e23fa9fc00aad89d8a8a3ee445
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947001"
---
# <a name="network-offload-and-optimization-technologies"></a>网络卸载和优化技术

在本主题中，我们概括介绍了 Windows Server 2016 中提供的不同网络卸载和优化功能，并讨论了它们如何帮助使网络更高效。 这些技术仅包括软件 (因此) 功能和技术、软件和硬件 (SH) 集成的功能和技术，以及仅 (的功能和技术。

Windows Server 2016 中提供的三个网络功能类别为：

1.  [软件仅 (因此) 功能和技术](hpn-software-only-features.md)：这些功能作为 OS 的一部分实现，并且独立于基础 NIC () 。 有时，这些功能需要对 NIC 进行某种优化才能实现最佳操作。 其中的示例包括 Hyper-v 功能，如 vmQoS、Acl 和非 Hyper-v 功能，如 NIC 组合。

2.  [软件和硬件 (SH) 集成功能和技术](hpn-software-hardware-features.md)：这些功能都具有软件和硬件组件。 该软件与它紧密功能所需的硬件功能相结合。 其中包括 VMMQ、VMQ、发送端 IPv4 校验和卸载以及 RSS。

3.  [仅限硬件 (哈) 功能和技术](hpn-hardware-only-features.md)：这些硬件加速可提高网络性能和软件，但不它紧密任何软件功能。 这些示例包括中断裁决、流控制和接收端 IPv4 校验和卸载。

4. [NIC 高级属性](hpn-nic-advanced-properties.md)：可以使用 get-netadapter Cmdlet 通过 Windows PowerShell 管理 nic 和所有功能。  你还可以使用网络控制面板 ( # A0) 来管理 Nic 和所有功能。

>[!TIP]
>- 因此，无论 NIC 速度或 NIC 功能如何，所有硬件体系结构中都提供了功能和技术。
>
>- 如果你的网络适配器支持这些功能或技术，则 SH 和 HO 功能才可用。

---