---
title: 子命令启动-服务器
description: 子命令启动-服务器的参考文章，用于启动 Windows 部署服务服务器的所有服务。
ms.topic: article
ms.assetid: 1e4343e2-0a16-4e65-8769-c09adaef5680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53fbc5ed80d69077efad49682368fbf3877361a0
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882062"
---
# <a name="subcommand-start-server"></a>子命令：启动-服务器

> 适用于： Windows Server (半年通道) ，Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

启动 Windows 部署服务服务器的所有服务。

## <a name="syntax"></a>语法
```
wdsutil [Options] /start-Server [/Server:<Server name>]
```
### <a name="parameters"></a>参数
|参数|描述|
|-------|--------|
|[/Server： <Server name> ]|指定要启动的服务器的名称。 此名称可以是 NetBIOS 名称，也可以是完全限定的域名 (FQDN) 。 如果未指定服务器名称，将使用本地服务器。|
## <a name="examples"></a>示例
若要启动服务器，请键入下列内容之一：
```
wdsutil /start-Server
wdsutil /verbose /start-Server /Server:MyWDSServer
```
## <a name="additional-references"></a>其他参考
- [命令行语法关键字](command-line-syntax-key.md) 
[使用 disable-Server 命令](using-the-disable-server-command.md) 
[使用 enable-Server 命令](using-the-enable-server-command.md) 
[使用 get-Server 命令](using-the-get-server-command.md) 
[使用 Initialize-Server 命令](using-the-initialize-server-command.md) 
[子命令：设置-服务器](subcommand-set-server.md) 
[子命令：停止-服务器](subcommand-stop-server.md) 
["取消初始化服务器" 选项](the-uninitialize-server-option.md)
