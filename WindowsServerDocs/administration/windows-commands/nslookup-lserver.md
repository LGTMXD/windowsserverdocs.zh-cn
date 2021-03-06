---
title: nslookup lserver
description: Nslookup lserver 命令的参考文章，此命令将初始服务器更改为指定的域名系统 (DNS) 域。
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ab7c478b6c9f3ae299559a556629e53f9eb852ee
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885793"
---
# <a name="nslookup-lserver"></a>nslookup lserver

> 适用于： Windows Server (半年通道) ，Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

将初始服务器更改为指定的域名系统 (DNS) 域。

此命令使用初始服务器来查找有关指定 DSN 域的信息。 如果要使用当前默认服务器查找信息，请使用[nslookup 服务器](nslookup-server.md)命令。

## <a name="syntax"></a>语法

```
lserver <DNSdomain>
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| --------- | ----------- |
| `<DNSdomain>` | 指定初始服务器的 DNS 域。 |
| /? | 在命令提示符下显示帮助。 |
| /help | 在命令提示符下显示帮助。 |

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [nslookup server](nslookup-server.md)
