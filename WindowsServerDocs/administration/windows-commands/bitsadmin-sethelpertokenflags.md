---
title: bitsadmin sethelpertokenflags
description: Bitsadmin sethelpertokenflags 命令的参考文章，用于设置与 BITS 传输作业关联的帮助程序令牌的使用标志。
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 1d3fee2b69ba498e3eae771b4be42848b1d88065
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893129"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

设置与 BITS 传输作业关联的帮助程序 [令牌](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)的用法标志   。

> [!NOTE]
> BITS 3.0 和更早版本不支持此命令。

## <a name="syntax"></a>语法

```
bitsadmin /sethelpertokenflags <job> <flags>
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| --------- | ----------- |
| 作业 (job) | 作业的显示名称或 GUID。 |
| flags | 可能的帮助程序令牌值，包括：<ul><li>**0x0001.** 用于打开上载作业的本地文件，创建或重命名下载作业的临时文件，或创建或重命名上传答复作业的答复文件。</li><li>**0x0002.** 用于打开服务器消息块的远程文件 (SMB) 上传或下载作业，或响应隐式 NTLM 或 Kerberos 凭据的 HTTP 服务器或代理质询。</li></ul>必须调用  `/setcredentialsjob targetscheme null null`   才能通过 HTTP 发送凭据。 |

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [bitsadmin 命令](bitsadmin.md)
