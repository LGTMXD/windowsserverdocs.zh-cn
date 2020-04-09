---
title: 初始化-服务器
description: 用于 Initialize-Server 的 Windows 命令主题，用于配置在安装服务器角色后初始使用的 Windows 部署服务服务器。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 68a26ad9-5eb2-4490-b782-b7cd46b8000d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c80af07827c889a3dd1c5d3050cd2ca3b4c8f1e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830790"
---
# <a name="initialize-server"></a>初始化-服务器

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

配置服务器角色后初始使用的 Windows 部署服务服务器。 运行此命令后，应使用 "[添加图像" 命令](using-the-add-image-command.md)命令向服务器中添加映像。
## <a name="syntax"></a>语法
```
wdsutil /Initialize-Server [/Server:<Server name>] /remInst:<Full path> [/Authorize]
```
### <a name="parameters"></a>参数
|参数|说明|
|-------|--------|
|[/Server：<Server name>]|指定服务器的名称。 此名称可以是 NetBIOS 名称或完全限定的域名（FQDN）。 如果未指定服务器名称，将使用本地服务器。|
|/remInst：<Full path>|指定 remoteInstall 文件夹的完整路径和名称。 如果指定的文件夹不存在，则此选项将在命令运行时创建该文件夹。 应始终输入本地路径，即使对于远程计算机也是如此。 例如： **D:\remoteInstall**。|
|/Authorize|在动态主机控制协议（DHCP）中授权服务器。 仅当启用了 DHCP rogue 检测时，此选项才是必需的，这意味着在提供客户端计算机之前，必须在 DHCP 中授权 Windows 部署服务 PXE 服务器。 请注意，默认情况下禁用 DHCP rogue 检测。|
## <a name="examples"></a><a name=BKMK_examples></a>示例
若要初始化服务器并将 remoteInstall 共享文件夹设置为 F：驱动器，请键入。
```
wdsutil /Initialize-Server /remInst:F:\remoteInstall
```
若要初始化服务器并将 remoteInstall 共享文件夹设置为 C：驱动器，请键入。
```
wdsutil /verbose /Progress /Initialize-Server /Server:MyWDSServer /remInst:C:\remoteInstall
```
## <a name="additional-references"></a>其他参考
- [命令行语法键](command-line-syntax-key.md)
[使用](using-the-disable-server-command.md)
使用[enable](using-the-enable-server-command.md) -server 命令
使用 Enable-Server[命令的命令](using-the-get-server-command.md)行语法键
[子命令： Set-server](subcommand-set-server.md)
子命令[：启动-服务器](subcommand-start-server.md)
子命令： [stop-server](subcommand-stop-server.md)
["取消初始化服务器" 选项](the-uninitialize-server-option.md)
