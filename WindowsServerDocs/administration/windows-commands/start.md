---
title: start
description: 适用于 start 的 Windows 命令主题，它启动单独的命令提示符窗口以运行指定的程序或命令。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0173f9b3-5cd7-4edb-b01e-d02193b4fadc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ab8fc07923a2396a173803264d54a036983fb71
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834070"
---
# <a name="start"></a>start

启动单独的命令提示符窗口以运行指定的程序或命令。

有关如何使用此命令的示例，请参阅[示例](#BKMK_examples)。

## <a name="syntax"></a>语法

```
start [<Title>] [/d <Path>] [/i] [{/min | /max}] [{/separate | /shared}] [{/low | /normal | /high | /realtime | /abovenormal | belownormal}] [/affinity <HexAffinity>] [/wait] [/elevate] [/b] [<Command> [<Parameter>... ] | <Program> [<Parameter>... ]]
```

### <a name="parameters"></a>参数

|参数|说明|
|---------|-----------|
|\<标题 >|指定要在命令提示符窗口标题栏中显示的标题。|
|/d \<路径 >|指定启动目录。|
|/i|将 Cmd.exe 启动环境传递到新的命令提示符窗口。 如果未指定 **/i** ，则使用当前环境。|
|/min \|/max|指定最小化（ **/min**）或最大化（ **/max**）新的命令提示符窗口。|
|/separate \|/shared|在单独的内存空间（ **/separate**）或共享内存空间（ **/shared**）中启动16位程序。 64位平台上不支持这些选项。|
|/low \|/normal \|/high \|/realtime \|/abovenormal \|/belownormal|启动指定优先级类中的应用程序。 有效的优先级类值为 **/low**、 **/normal**、 **/high**、 **/realtime**、 **/abovenormal**和 **/belownormal**。|
|/affinity \<HexAffinity >|将指定的处理器关联掩码（表示为十六进制数）应用于新应用程序。|
|/wait|启动应用程序并等待其结束。|
|/elevate|以管理员身份运行应用程序。|
|/b|启动应用程序而不打开新的命令提示符窗口。 除非应用程序启用了 CTRL + C 处理，否则将忽略 CTRL + C 处理。 使用 CTRL + BREAK 中断应用程序。|
|\<命令 > \| \<程序 >|指定要启动的命令或程序。|
|\<参数 > 。|指定要传递给命令或程序的参数。|
|/?|在命令提示符下显示帮助。|

## <a name="remarks"></a>备注

- 您可以通过将文件的名称键入为命令，通过文件关联来运行不可执行文件。
- 当你在不带扩展名或路径限定符的情况下运行包含字符串 CMD 的命令时，CMD 将替换为 COMSPEC 变量的值。 这会阻止用户从当前目录中提取**cmd** 。
- 运行32位图形用户界面（GUI）应用程序时， **cmd**在返回到命令提示符之前不等待应用程序退出。 如果从命令脚本运行应用程序，则不会发生此行为。
- 当你运行使用不包含扩展的第一个令牌的命令时，Cmd.exe 将使用 PATHEXT 环境变量的值来确定要查找的扩展以及顺序。 PATHEXT 变量的默认值为：  
  ```
  .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC 
  ```  
  请注意，语法与 PATH 变量相同，每个扩展名用分号分隔。
- 当它搜索可执行文件时，如果任何扩展上都没有匹配项，则**开始**检查该名称是否与目录名称匹配。 如果是这样，请在该路径上**打开 "资源**管理器"。

## <a name="examples"></a><a name=BKMK_examples></a>示例

若要在命令提示符下启动 Myapp 程序并保留使用当前的 "命令提示符" 窗口，请键入：
```
start myapp 
```
若要在单独的最大化命令提示符窗口中查看**启动**命令行帮助主题，请键入：
```
start /max start /?
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)
