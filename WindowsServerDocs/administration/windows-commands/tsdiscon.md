---
title: tsdiscon
description: Tsdiscon 的参考主题，用于断开会话与远程桌面会话主机服务器的连接。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2a97d1b157445fd43acce5a80f3d793ed5ae5af
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721265"
---
# <a name="tsdiscon"></a>tsdiscon

> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

断开会话与远程桌面会话主机服务器的连接。



> [!NOTE]
> 在 Windows Server 2008 R2 中，终端服务被重命名为远程桌面服务。 若要了解最新版本中的新增功能，请参阅 Windows server TechNet 库中的[Windows server 2012 远程桌面服务中的新增功能](https://technet.microsoft.com/library/hh831527)。

## <a name="syntax"></a>语法
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>参数

|参数|描述|
|-------|--------|
|\<SessionId>|指定要断开连接的会话的 ID。|
|\<SessionName>|指定要断开连接的会话的名称。|
|/server：\<ServerName>|指定包含要断开连接的会话的终端服务器。 否则，使用当前的 rd 会话主机服务器。|
|/v|显示要执行的操作的相关信息。|
|/?|在命令提示符下显示帮助。|

## <a name="remarks"></a>备注
-   您必须拥有 "完全控制" 权限或 "断开连接" 特殊访问权限才能断开其他用户与会话的连接。
-   如果未指定会话 ID 或会话名称， **tsdiscon**将断开当前会话的连接。
-   断开会话时运行的任何应用程序都将在您重新连接到该会话时自动运行，而不会丢失数据。 使用 "**重置会话**" 结束已断开连接的会话的正在运行的应用程序，但请注意，这可能会导致会话中的数据丢失。
-   仅当从远程服务器使用**tsdiscon**时， **/server**参数才是必需的。
-   无法断开控制台会话的连接。

## <a name="examples"></a>示例
- 若要断开当前会话，请键入：
  ```
  tsdiscon
  ```
- 若要断开会话10，请键入：
  ```
  tsdiscon 10
  ```
- 若要断开名为 TERM04 的会话，请键入：
  ```
  tsdiscon TERM04
  ```
  ## <a name="additional-references"></a>其他参考
  - [命令行语法键](command-line-syntax-key.md)
  [远程桌面服务（终端服务）命令参考](remote-desktop-services-terminal-services-command-reference.md)
