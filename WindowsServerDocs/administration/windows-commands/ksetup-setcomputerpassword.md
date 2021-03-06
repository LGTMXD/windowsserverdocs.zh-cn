---
title: ksetup setcomputerpassword
description: Ksetup setcomputerpassword 命令的参考文章，用于设置本地计算机的密码。
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d9dba34490616b07671ada16e0c76f0122c3d6a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887772"
---
# <a name="ksetup-setcomputerpassword"></a>ksetup setcomputerpassword

设置本地计算机的密码。 此命令仅影响计算机帐户，需要重新启动才能使密码更改生效。

> [!IMPORTANT]
> 计算机帐户密码不会在注册表中显示，也不会显示为**ksetup**命令的输出。

## <a name="syntax"></a>语法

```
ksetup /setcomputerpassword <password>
```

### <a name="parameters"></a>参数

| 参数 | 描述 |
| --------- | ----------- |
| `<password>` | 指定提供的密码以设置本地计算机上的计算机帐户。 只能使用具有管理权限的帐户来设置密码，并且密码必须为1到156个字母数字或特殊字符。 |

### <a name="examples"></a>示例

若要将本地计算机上的计算机帐户密码从*IPops897*更改为*IPop $ 897！*，请键入：

```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [ksetup 命令](ksetup.md)
