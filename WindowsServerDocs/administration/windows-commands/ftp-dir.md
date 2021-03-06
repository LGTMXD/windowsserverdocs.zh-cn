---
title: ftp dir
description: Ftp dir 命令的参考文章，其中显示了远程计算机上的目录文件和子目录的列表。
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a4f65cee67ec91b6871649fece4f580684c2e3f
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87889476"
---
# <a name="ftp-dir"></a>ftp dir

> 适用于： Windows Server (半年通道) ，Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

显示远程计算机上的目录文件和子目录的列表。

## <a name="syntax"></a>语法

```
dir [<remotedirectory>] [<localfile>]
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| ------- | -------- |
| `[<remotedirectory>]` | 指定要查看其列表的目录。 如果未指定目录，则使用远程计算机上的当前工作目录。 |
| `[<localfile>]` | 指定要在其中存储目录列表的本地文件。 如果未指定本地文件，则结果将显示在屏幕上。 |

### <a name="examples"></a>示例

若要在远程计算机上显示*dir1*的目录列表，请键入：

```
dir dir1
```

若要将远程计算机上的当前目录列表保存*dirlist.txt*本地文件，请键入：

```
dir . dirlist.txt
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [其他 FTP 指南](/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
