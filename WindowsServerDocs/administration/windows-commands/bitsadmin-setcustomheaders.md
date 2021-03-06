---
title: bitsadmin setcustomheaders
description: Bitsadmin setcustomheaders 命令的参考文章，可将自定义 HTTP 标头添加到 GET 请求。
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 407e4aa85d8413167add716cd63fe620f73b0e12
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893181"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

向发送到 HTTP 服务器的 GET 请求添加自定义 HTTP 标头。 有关 GET 请求的详细信息，请参阅[方法定义](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3)和[标头字段定义](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)。

## <a name="syntax"></a>语法

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| --------- | ----------- |
| 作业 (job) | 作业的显示名称或 GUID。 |
| `<header1> <header2>`依此类推 | 作业的自定义标头。 |

## <a name="examples"></a>示例

若要为名为*myDownloadJob*的作业添加自定义 HTTP 标头：

```
bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [bitsadmin 命令](bitsadmin.md)
