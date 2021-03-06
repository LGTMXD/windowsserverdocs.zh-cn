---
title: bitsadmin setpeercachingflags
description: Bitsadmin setpeercachingflags 命令的参考文章，用于设置标志，这些标志确定是否可以缓存作业的文件并将其提供给对等方以及作业是否可以从对等方下载内容。
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73135ed6f08962cbe73aad4765dc4d3b4f7ff958
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892979"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

设置标志，该标志确定是否可以缓存作业的文件并将其提供给对等方以及作业是否可以从对等方下载内容。

## <a name="syntax"></a>语法

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| --------- | ----------- |
| 作业 (job) | 作业的显示名称或 GUID。 |
| 值 | 无符号整数，其中包括：<ul><li>**1.** 作业可以从对等方下载内容。</li><li>**2.** 该作业的文件可以缓存并提供给对等方。</li></ul> |

## <a name="examples"></a>示例

允许名为*myDownloadJob*的作业从对等方下载内容：

```
bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [bitsadmin 命令](bitsadmin.md)
