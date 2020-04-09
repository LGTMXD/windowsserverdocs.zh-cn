---
title: find
description: 适用于 * * * * 的 Windows 命令主题
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ca66b22-3b7c-4166-8503-eb75fc53ab46
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 82b966db4117e9273ae6aed8d30baec76362de2f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844690"
---
# <a name="find"></a>find



搜索文件中的文本字符串，并显示包含指定字符串的文本行。

有关如何使用此命令的示例，请参阅[示例](#BKMK_examples)。

## <a name="syntax"></a>语法

```
find [/v] [/c] [/n] [/i] [/off[line]] <String> [[<Drive>:][<Path>]<FileName>[...]]
```

### <a name="parameters"></a>参数

|           参数           |                                              说明                                               |
|-------------------------------|--------------------------------------------------------------------------------------------------------|
|              /v               |                    显示不包含指定 \<字符串 > 的所有行。                     |
|              /c               |              计算包含指定 \<字符串 > 的行并显示总计。              |
|              /n               |                            每行的前面都有文件的行号。                             |
|              /i               |                            指定搜索不区分大小写。                            |
|         [/off [line]]          |                        不会跳过设置了脱机属性的文件。                        |
|          \<字符串 >          | 必需。 指定要搜索的字符组（用引号引起来）。 |
| [\<驱动器 >：][<Path>]<FileName> |        指定要在其中搜索指定字符串的文件的位置和名称。        |
|              /?               |                                  在命令提示符下显示帮助。                                  |

## <a name="remarks"></a>备注

-   指定字符串

    如果不使用 **/i**，请**查找**确切搜索指定的*字符串*。 例如， **find**命令以不同的方式对待字符 a 和。 但是，如果使用 **/i**，则**find**不区分大小写，并且会将和视为相同的字符。

    如果要搜索的字符串包含引号，则必须对字符串中包含的每个引号使用双引号（例如，此字符串包含引号）。
-   使用 "**查找**" 作为筛选器

    如果省略文件名， **find**将充当筛选器，采用标准输入源（通常是键盘、管道（|）或重定向文件）输入，然后显示包含*字符串*的任何行。
-   排序命令语法

    可以按任意顺序键入**find**命令的参数和命令行选项。
-   使用通配符

    不能在使用 " **&#42;** **查找**" 命令指定的文件名或扩展名中使用通配符（和 **？** ）。 若要在使用通配符指定的一组文件中搜索字符串，可以在**for**命令中使用 "**查找**" 命令。
-   将 **/v**或 **/n**与 **/c**一起使用

    如果在同一命令行中使用 **/c**和 **/v** ， **find**将显示不包含指定字符串的行的计数。 如果在同一命令行中指定 **/c**和 **/n** ， **find**将忽略 **/n**。
-   使用带有回车的**查找**

    "**查找**" 命令无法识别回车符。 使用 "**查找**" 在包含回车符的文件中搜索文本时，必须将搜索字符串限制为可在回车符之间找到的文本（即，不太可能会被回车符中断的字符串）。 例如，如果字词和文件之间发生回车符，则 "**查找**" 不会报告该字符串的匹配项。

## <a name="examples"></a><a name=BKMK_examples></a>示例

若要显示 Pencil.ad 中包含字符串 "Sharpener" 的所有行，请键入：
```
find Pencil Sharpener pencil.ad
```
若要在引号内查找包含文本的字符串，必须将整个字符串用引号引起来。 那么，对于字符串中包含的每个引号，都必须使用两个引号。 查找标记为仅用于讨论的科学家。 它不是最终报表。 在 "报表" 中，键入：
```
find The scientists labeled their paper for discussion only. It is not a final report. report.doc
```
如果要搜索一组文件，则可以使用中的 "**查找** **" 命令**。 若要在当前目录中搜索扩展名为 .bat 且包含字符串提示符的文件，请键入：
```
for %f in (*.bat) do find PROMPT %f 
```
若要在硬盘上搜索并显示包含字符串 CPU 的驱动器 C 上的文件名，请使用竖线（|）将**dir**命令的输出定向到**find**命令，如下所示：
```
dir c:\ /s /b | find CPU 
```
因为**查找**搜索区分大小写，而**dir**产生大写输出，所以必须以大写字母键入字符串 CPU，或将 **/i**命令行选项与**find**一起使用。

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)