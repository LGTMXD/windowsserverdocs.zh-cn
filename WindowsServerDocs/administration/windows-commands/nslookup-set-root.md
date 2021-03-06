---
title: nslookup set root
description: Nslookup set root 命令的参考文章，它更改用于查询的根服务器的名称。
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 69dd99b00e186a4338ec5c176d8fed128325b89e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885524"
---
# <a name="nslookup-set-root"></a>nslookup set root

> 适用于： Windows Server (半年通道) ，Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

更改用于查询的根服务器的名称。

> [!NOTE]
> 此命令支持[nslookup 根](nslookup-root.md)命令。

## <a name="syntax"></a>语法

```
set root=<rootserver>
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| ---------- | ---------- |
| `<rootserver>` | 指定根服务器的新名称。 默认值为**ns.nic.ddn.mil**。 |
| /? | 在命令提示符下显示帮助。 |
| /help | 在命令提示符下显示帮助。 |

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [nslookup root](nslookup-root.md)
