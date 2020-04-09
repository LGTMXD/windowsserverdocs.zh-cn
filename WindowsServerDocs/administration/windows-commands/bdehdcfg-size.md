---
title: bdehdcfg 大小
description: '**Bdehdcfg size**的 Windows 命令主题，它指定在创建新的系统驱动器时系统分区的大小。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c72bdfd0b8bf4dfd0aa36885ceb7fd249a18c332
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851020"
---
# <a name="bdehdcfg-size"></a>bdehdcfg： size

指定在创建新的系统驱动器时的系统分区大小。

有关如何使用此命令的示例，请参阅[示例](#BKMK_Examples)。

## <a name="syntax"></a>语法

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink} -size <SizeinMB>
```

#### <a name="parameters"></a>参数

| 参数 | 说明 |
| --------- | ----------- |
| `<SizeinMB>` | 指示用于新分区的兆字节数（MB）。 |

## <a name="remarks"></a>备注

如果未指定大小，则该工具将使用默认值 300 MB。 系统驱动器的最小大小为 100 MB。 如果要将系统恢复或其他系统工具存储在系统分区上，则应相应地增加大小。

> [!NOTE]
> **Size**命令不能与**target** `<DriveLetter>` **merge**命令组合。

## <a name="examples"></a><a name=BKMK_Examples></a>示例

下面的示例演示如何使用**size**命令将 500 MB 分配给默认系统驱动器。

```
bdehdcfg -target default -size 500
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)