---
title: pause
description: 用于暂停批处理程序处理的 "暂停" 命令的参考文章。
ms.topic: article
ms.assetid: cab3afc3-d046-432f-a0bf-6282f0099032
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5f8f10ae64fea8cf2c4610247ebe28b03ce26ae
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885062"
---
# <a name="pause"></a>pause

暂停批处理程序的处理，并显示提示，`Press any key to continue . . .`

## <a name="syntax"></a>语法

```
pause
```

### <a name="parameters"></a>参数

| 参数 | 说明 |
|--|--|
| /? | 在命令提示符下显示帮助。 |

## <a name="remarks"></a>备注

- 如果按 CTRL + C 停止批处理程序，将显示以下消息： `Terminate batch job (Y/N)?` 。 如果按**Y** (为 "是") 响应此消息，批处理程序将结束并控制返回到操作系统。

- 可以在可能不希望处理的批处理文件的一部分之前插入**pause**命令。 当**暂停暂停**批处理程序的处理时，可以按 CTRL + C，然后按**Y**停止批处理程序。

## <a name="examples"></a>示例

若要创建一个批处理程序来提示用户更改其中一个驱动器中的磁盘，请键入：

```
@echo off
:Begin
copy a:*.*
echo Put a new disk into Drive A
pause
goto begin
```

在此示例中，驱动器 A 中的磁盘上的所有文件都复制到当前目录中。 在该消息提示你将新磁盘放入驱动器 A 后， **pause**命令将挂起处理，以便你可以更改磁盘，然后按任意键继续处理。 此批处理程序在无穷循环中运行- **goto begin**命令将命令解释器发送到批处理文件的开始标签。

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)