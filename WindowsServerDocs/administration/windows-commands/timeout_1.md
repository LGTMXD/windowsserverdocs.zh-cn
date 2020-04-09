---
title: timeout
description: 针对超时的 Windows 命令主题，用于在指定的秒数内暂停命令处理器。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e26b4a84-0e30-46e1-aa10-0667b7d3cb4c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd0a43e49e8a7567ac975333b04a9e6f549a0fd8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832810"
---
# <a name="timeout"></a>timeout

在指定的秒数内暂停命令处理器。

有关如何使用此命令的示例，请参阅[示例](#BKMK_examples)。

## <a name="syntax"></a>语法

```
timeout /t <TimeoutInSeconds> [/nobreak] 
```

### <a name="parameters"></a>参数

|参数|说明|
|---------|-----------|
|/t \<TimeoutInSeconds >|指定命令处理器继续处理之前要等待的秒数（-1 到99999）。 值-1 会使计算机无限期等待击键。|
|/nobreak|指定忽略用户密钥笔划。|
|/?|在命令提示符下显示帮助。|

## <a name="remarks"></a>备注

-   **Timeout**命令通常在批处理文件中使用。
-   即使超时期限未过期，用户按键也会立即继续执行命令处理器。
-   与 "**睡眠**" 命令结合使用时，"**超时**" 类似于 "**暂停**" 命令。

## <a name="examples"></a><a name=BKMK_examples></a>示例

若要将命令处理器暂停10秒，请键入：
```
timeout /t 10
```
若要将命令处理器暂停100秒并忽略任何击键，请键入：
```
timeout /t 100 /nobreak
```
若要在按下某个键之前无限期暂停命令处理器，请键入：
```
timeout /t -1
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)
