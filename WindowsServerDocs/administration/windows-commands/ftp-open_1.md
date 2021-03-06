---
title: ftp open
description: 用于连接到指定 ftp 服务器的 ftp open 命令的参考文章。
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd80ef5a8a3e4efa36a5fce0d228fd01f3a26bdc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889149"
---
# <a name="ftp-open"></a>ftp open

> 适用于： Windows Server (半年通道) ，Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

连接到指定的 ftp 服务器。

## <a name="syntax"></a>语法

```
open <computer> [<port>]
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| --------- | ----------- |
| `<computer>` | 指定您尝试连接到的远程计算机。 您可以使用 IP 地址或计算机名称 (在这种情况下，DNS 服务器或主机文件必须) 可用。 |
| `[<port>]` | 指定用于连接到 ftp 服务器的 TCP 端口号。 默认情况下，使用 TCP 端口21。 |

### <a name="examples"></a>示例

若要在*ftp.microsoft.com*连接到 ftp 服务器，请键入：

```
open ftp.microsoft.com
```

若要连接到侦听 TCP 端口*755*的*ftp.microsoft.com*上的 ftp 服务器，请键入：

```
open ftp.microsoft.com 755
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [其他 FTP 指南](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
