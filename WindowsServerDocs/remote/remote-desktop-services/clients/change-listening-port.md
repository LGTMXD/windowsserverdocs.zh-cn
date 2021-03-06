---
title: 更改远程桌面的侦听端口
description: 了解如何更改远程桌面客户端的侦听端口。
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0add2c2d577c475044064394b7bd77e5eab5d802
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958105"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>更改计算机上的远程桌面的侦听端口

>适用于：Windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2008 R2

通过远程桌面客户端连接到计算机（Windows 客户端或 Windows Server）时，计算机上的远程桌面功能会通过定义的侦听端口（默认情况下为 3389）“侦听”连接请求。 可以通过修改注册表来更改 Windows 计算机上的侦听端口。

1. 启动注册表编辑器。 （在“搜索”框中键入 regedit。）
2. 导航到以下注册表子项：HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. 单击“编辑”>“修改”  ，然后单击“十进制”  。
4. 键入新端口号，然后单击“确定”  。
5. 关闭注册表编辑器，然后重新启动计算机。

下次使用远程桌面连接连接到此计算机时，必须键入新端口。 如果正在使用防火墙，请确保将防火墙配置为允许连接到新端口号。
