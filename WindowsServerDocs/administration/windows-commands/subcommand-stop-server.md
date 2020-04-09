---
title: 子命令停止-服务器
description: "\"子命令停止-服务器\" 的 Windows 命令主题，它停止 Windows 部署服务服务器上的所有服务。"
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 09f411c0-099f-4591-95fd-b77b3fd9118a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2671e7a2c2e5bb542cecd9374ad6364d68ff5bd4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833710"
---
# <a name="subcommand-stop-server"></a>子命令：停止-服务器

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

停止 Windows 部署服务服务器上的所有服务。

## <a name="syntax"></a>语法
```
wdsutil [Options] /Stop-Server [/Server:<Server name>]
```
### <a name="parameters"></a>参数
|参数|说明|
|-------|--------|
|[/Server：<Server name>]|指定服务器的名称。 此名称可以是 NetBIOS 名称或完全限定的域名（FQDN）。 如果未指定服务器名称，将使用本地服务器。|
## <a name="examples"></a><a name=BKMK_examples></a>示例
若要停止服务，请键入下列内容之一：
```
wdsutil /Stop-Server
wdsutil /verbose /Stop-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>其他参考
- [命令行语法键](command-line-syntax-key.md)
[使用](using-the-disable-server-command.md)
使用[enable](using-the-enable-server-command.md) -server 命令
使用 "服务器[" 命令的](using-the-get-server-command.md)命令行语法，
使用 "[初始化-](using-the-initialize-server-command.md)服务器" 命令
子命令： [Set-](subcommand-set-server.md) server
[子命令：启动-服务器](subcommand-start-server.md)
["取消初始化-服务器" 选项](the-uninitialize-server-option.md)
