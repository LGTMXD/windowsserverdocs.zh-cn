---
title: bcdboot
description: Bcdboot 命令的参考主题，可快速设置系统分区，或修复位于系统分区上的启动环境。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cde91738f524350f72f0278495e4bd46a3960e6f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718703"
---
# <a name="bcdboot"></a>bcdboot

使你能够快速设置系统分区，或修复位于系统分区上的启动环境。 系统分区是通过将一组简单的引导配置数据（BCD）文件复制到现有的空分区来设置的。

## <a name="syntax"></a>语法

```
bcdboot <source> [/l] [/s]
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| --------- | ----------- |
| source | 指定用作复制启动环境文件的源的 Windows 目录的位置。 |
| /l | 指定区域设置。 默认区域设置为美国英语。 |
| /s | 指定系统分区的卷号。 默认值为固件标识的系统分区。 |

## <a name="examples"></a>示例

有关在何处查找 BCDboot 的信息以及如何使用此命令的示例，请参阅[BCDboot 命令行选项](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824874(v=win.10)x)主题。

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)
