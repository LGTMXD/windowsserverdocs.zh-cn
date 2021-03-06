---
title: exec
description: 用于在本地计算机上运行脚本文件的 exec 命令的参考文章。
ms.topic: article
ms.assetid: 364e8baf-576f-401b-a431-7d3c06621614
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d0fd297ca3b5908a6782379dbd716098e47f751
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890488"
---
# <a name="exec"></a>exec

在本地计算机上运行脚本文件。 此命令还在备份或还原顺序中复制或还原数据。 如果脚本失败，将返回错误，并且 DiskShadow 将退出。

该文件可以是**cmd**脚本。

## <a name="syntax"></a>语法

```
exec <scriptfile.cmd>
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| --------- | ----------- |
| `<scriptfile.cmd>` | 指定要运行的脚本文件。 |

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [diskshadow 命令](diskshadow.md)
