---
title: Windows Server 版本 1809 中的新增功能
description: Windows Server 版本 1809 中的新功能
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.localizationpriority: high
ms.openlocfilehash: cb3bf10b0c89f60a5cebb7109ebc4a7de46f8961
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941636"
---
# <a name="whats-new-in-windows-server-version-1809"></a>Windows Server 版本 1809 中的新增功能

>适用于：Windows Server（半年频道）

若要了解 Windows 中的最新功能，请参阅 [Windows Server 中的新增功能](whats-new-in-windows-server.md)。 本主题将介绍 Windows Server 版本 1809 中的一些新功能。

## <a name="container-networking-with-kubernetes"></a>支持 Kubernetes 的容器网络

Windows Server 2019 中[支持 Kubernetes 的容器网络](../networking/sdn/technologies/containers/container-networking-overview.md)通过增强平台网络复原和容器网络插件支持极大地提高了 Windows 上 Kubernetes 的可用性。
此外，客户可在 Kubernetes 网络安全性的基础上部署工作负荷来保护使用嵌入工具的 Linux 和 Windows 服务。

## <a name="group-managed-service-accounts-for-containers"></a>适用于容器的组托管服务帐户

Windows Server 版本 1809 针对使用组托管服务帐户 (gMSA) 来访问网络资源的容器提高了可扩展性和可靠性。

## <a name="host-device-access-for-containers"></a>适用于容器的主机设备访问

可为进程隔离的 Windows Server 容器分配简单总线。
在需要通过 SPI、I2C、GPIO 和 UART/COM 进行通信的容器中运行的应用程序现在可执行此操作。

## <a name="additional-features"></a>其他功能
除了 Windows Server 版本 1809 中的新增功能，[Windows Server 2019](../get-started-19/get-started-19.md) 的以下新特性和功能也适用于 Windows Server 版本 1809：

* 容器改进
* HTTP/2
* Kubernetes 支持
* Windows 上的 Linux 容器
* [低额外延迟后台传输 (LEDBAT)](https://techcommunity.microsoft.com/t5/networking-blog/bg-p/NetworkingBlog)
* 虚拟工作负荷的网络性能提升
* [Server Core 应用兼容性按需功能 (FOD)](../get-started-19/install-fod-19.md)
* [存储迁移服务 (SMS)](../storage/whats-new-in-storage.md#storage-spaces-direct)
* 存储副本
* 系统见解
* Windows Defender 高级威胁防护 (ATP)
* Windows Defender ATP 攻击防护
* [Windows 时间服务](../networking/windows-time-service/insider-preview.md)
