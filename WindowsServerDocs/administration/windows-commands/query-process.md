---
title: 查询进程
description: 适用于 * * * * 的 Windows 命令主题
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ee42286691444c3a667801be3174514a81441c6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836960"
---
# <a name="query-process"></a>查询进程

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

显示有关在远程桌面会话主机（rd 会话主机）服务器上运行的进程的信息。
您可以使用此命令来找出特定用户正在运行的程序，以及哪些用户在运行特定程序。
有关如何使用此命令的示例，请参阅[示例](#BKMK_examples)。
> [!NOTE]
> 在 Windows Server 2008 R2 中，“终端服务”被重命名为“远程桌面服务”。 若要了解最新版本中的新增功能，请参阅 Windows server TechNet 库中的[Windows server 2012 远程桌面服务中的新增功能](https://technet.microsoft.com/library/hh831527)。
> ## <a name="syntax"></a>语法
> ```
> query process [* | <ProcessID> | <UserName> | <SessionName> | /id:<nn> | <ProgramName>] [/server:<ServerName>]
> ```
> ### <a name="parameters"></a>参数
> 
> |      参数       |                                                                 说明                                                                  |
> |----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
> |          \*          |                                                    列出所有会话的进程。                                                     |
> |     <ProcessID>      |                                   指定标识要查询的进程的数字 ID。                                   |
> |      <UserName>      |                                       指定要列出其进程的用户的名称。                                       |
> |    <SessionName>     |                                     指定要列出其进程的会话的名称。                                      |
> |       /id：<nn>       |                                      指定要列出其进程的会话的 ID。                                       |
> |    <ProgramName>     |                     指定要查询其进程的程序的名称。 .Exe 扩展名是必需的。                     |
> | /server:<ServerName> | 指定要列出其进程的 rd 会话主机服务器。 如果未指定，则使用你当前登录到的服务器。 |
> |          /?          |                                                     在命令提示符下显示帮助。                                                     |
> 
> ## <a name="remarks"></a>备注
> - 管理员对所有**查询处理**函数具有完全访问权限。
> - 如果未指定 < 用户名 >、<*会话* *名称*>、 **/id：** <*nn*>、<*ProgramName*> 或 **\\** * 参数，则**query process**只显示属于当前用户的进程。
> - 如果指定了会话，则它必须标识活动会话。
> - **查询过程**返回以下信息：
>   -   拥有此进程的用户
>   -   拥有进程的会话
>   -   会话的 ID
>   -   进程的名称
>   -   进程的 ID
> - 当**查询过程**返回信息时，将在每个属于当前会话的进程之前显示大于号（>）。
>   ## <a name="examples"></a><a name=BKMK_examples></a>示例
> - 若要显示有关所有会话正在使用的进程的信息，请键入：
>   ```
>   query process *
>   ```
> - 若要显示有关会话 ID 2 使用的进程的信息，请键入：
>   ```
>   query process /ID:2
>   ```
>   ## <a name="additional-references"></a>其他参考
>   - [命令行语法键](command-line-syntax-key.md)
>   [query](query.md)
>   [远程桌面服务（终端服务）命令参考](remote-desktop-services-terminal-services-command-reference.md)
