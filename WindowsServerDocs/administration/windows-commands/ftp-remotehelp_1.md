---
title: ftp remotehelp
description: Ftp remotehelp 命令的参考文章，其中显示了有关远程命令的帮助。
ms.topic: article
ms.assetid: ef23adf3-ead4-44c8-ac1d-c8a6f4b2bf73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e428a43ddcf36f1125c3fa83ddeeeff3cae979d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889016"
---
# <a name="ftp-remotehelp"></a>ftp remotehelp

> 适用于： Windows Server (半年通道) ，Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

显示远程命令的帮助。

## <a name="syntax"></a>语法

```
remotehelp [<command>]
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| ------- | -------- |
| `[<command>]` | 指定需要帮助的命令的名称。 如果 `<command>` 未指定，则此命令将显示所有远程命令的列表。 还可以使用[ftp 引号](ftp-quote.md)或[ftp 文本](ftp-literal_1.md)运行远程命令。 |

### <a name="examples"></a>示例

若要显示远程命令的列表，请键入：

```
remotehelp
```

若要显示适用于 "*远程操作" 命令*的语法，请键入：

```
remotehelp feat
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [ftp quote](ftp-quote.md)

- [ftp literal](ftp-literal_1.md)

- [其他 FTP 指南](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
