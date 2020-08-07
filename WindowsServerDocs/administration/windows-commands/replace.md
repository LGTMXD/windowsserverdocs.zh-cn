---
title: replace
description: 了解如何使用 replace 命令替换文件。
ms.topic: article
ms.assetid: 6143661e-d90f-4812-b265-6669b567dd1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 34d1adfc6a92dce33a6a9bbac308d3338db3934e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883679"
---
# <a name="replace"></a>replace



替换文件。 如果与 **/a**选项一起使用，请**替换**将新文件添加到目录，而不是替换现有文件。



## <a name="syntax"></a>语法

```
replace [<Drive1>:][<Path1>]<FileName> [<Drive2>:][<Path2>] [/a] [/p] [/r] [/w]
replace [<Drive1>:][<Path1>]<FileName> [<Drive2>:][<Path2>] [/p] [/r] [/s] [/w] [/u]
```

### <a name="parameters"></a>参数

|参数|描述|
|---------|-----------|
|[\<Drive1>:][\<Path1>]\<FileName>|指定源文件或文件集的位置和名称。 *FileName*是必需的，并且可以包括 (**&#42;** 和 **？**) 的通配符。|
|[\<Drive2>:][\<Path2>]|指定目标文件的位置。 不能为替换的文件指定文件名。 如果未指定驱动器或路径， **replace**将使用当前驱动器和目录作为目标。|
|/a|将新文件添加到目标目录，而不是替换现有文件。 不能将此命令行选项与 **/s**或 **/u**命令行选项一起使用。|
|/p|在替换目标文件或添加源文件之前，提示你进行确认。|
|/r|替换只读和未受保护的文件。 如果尝试替换只读文件，但未指定 **/r**，则会产生错误并停止替换操作。|
|/W|在搜索源文件开始之前，请等待你插入磁盘。 如果未指定 **/w**，请在按 enter 后立即**替换**或添加文件。|
|/s|搜索目标目录中的所有子目录并替换匹配文件。 不能将 **/s**与 **/a**命令行选项一起使用。 **Replace**命令不搜索*Path1*中指定的子目录。|
|/U|仅替换目标目录中比源目录中的文件旧的那些文件。 不能将 **/u**与 **/a**命令行选项一起使用。|
|/?|在命令提示符下显示帮助。|

## <a name="remarks"></a>备注

- "**替换**" 添加或替换文件，文件名显示在屏幕上。 **替换**完成后，将按以下格式之一显示摘要行：
  ```
  nnn files added
  nnn files replaced
  no file added
  no file replaced
  ```
- 如果你使用的是软盘并且需要在 "**替换**" 操作过程中切换磁盘，则可以指定 " **/w** " 命令行选项，以便 "**替换**" 将等待你切换磁盘。
- 不能使用**replace**来更新隐藏的文件或系统文件。
- 下表显示了每个退出代码及其含义的简短说明：
  |退出代码|说明|
  |---------|-----------|
  |0|**Replace**命令已成功替换或添加文件。|
  |1|**Replace**命令遇到了不正确的 MS-DOS 版本。|
  |2|**Replace**命令找不到源文件。|
  |3|**Replace**命令找不到源或目标路径。|
  |5|用户无权访问要替换的文件。|
  |8|系统内存不足，无法执行该命令。|
  |11|用户在命令行上使用了错误的语法。|

> [!NOTE]
> 可以在批处理程序的**if**命令行中使用 ERRORLEVEL 参数来处理**replace**返回的退出代码。

## <a name="examples"></a><a name="BKMK_examples"></a>示例

若要更新在驱动器) C 上的多个目录中显示的名为 " (" 的文件的所有版本，请在驱动器 A 中的软盘上键入以下内容：

`replace a:\phones.cli c:\ /s`

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)