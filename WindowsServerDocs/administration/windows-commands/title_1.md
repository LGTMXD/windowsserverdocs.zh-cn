---
title: title
description: 标题参考文章，用于为 "命令提示符" 窗口创建标题。
ms.topic: article
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3fede3a0f71da2913e798852817722eaea414770
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881389"
---
# <a name="title"></a>title

创建 "命令提示符" 窗口的标题。



## <a name="syntax"></a>语法

```
title [<String>]
```

### <a name="parameters"></a>参数

|参数|描述|
|---------|-----------|
|\<String>|指定 "命令提示符" 窗口的标题。|
|/?|在命令提示符下显示帮助。|

## <a name="remarks"></a>备注

-   若要为批处理程序创建窗口标题，请在批处理程序的开头包含**title**命令。
-   设置窗口标题后，只能使用**title**命令对其进行重置。

## <a name="examples"></a>示例

在下面的示例脚本中，命令提示符窗口的标题将更改为在批处理文件执行**复制**命令时更新文件。 执行命令后，将 `Files Updated` 显示文本，并且命令提示符窗口的标题将更改回命令提示符。
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)