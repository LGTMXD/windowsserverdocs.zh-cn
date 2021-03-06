---
title: select partition
description: '* * * * 的参考文章'
ms.topic: article
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c144bc3271fa4d10dfc006d8c08e1a737f763fe
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882856"
---
# <a name="select-partition"></a>select partition

> 适用于： Windows Server (半年通道) ，Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

选择指定分区并将焦点移到该分区。 此命令还可用于显示当前在所选磁盘中有焦点的分区。



## <a name="syntax"></a>语法

```
select partition=<n>
```

### <a name="parameters"></a>参数

|   参数    |                                                                                    描述                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 依据\=<n> | 要接收焦点的分区号。 通过使用 DiskPart 中的 "**列出分区**" 命令，你可以查看当前所选磁盘上的所有分区的编号。 |

## <a name="remarks"></a>备注

-   必须先使用 "**选择磁盘**" 命令选择一个磁盘，然后才能选择分区。

-   如果未指定分区号，则此命令将显示当前在所选磁盘中有焦点的分区。

-   如果选择了包含相应分区的卷，则会自动选择该分区。

-   如果使用相应的卷选择了分区，则会自动选择该卷。

## <a name="examples"></a>示例
若要将焦点移动到第3分区，请键入：

```
select partitition=3
```

若要在所选磁盘中显示当前具有焦点的分区，请键入：

```
select partition
```

## <a name="additional-references"></a>其他参考
- [命令行语法项](command-line-syntax-key.md)




