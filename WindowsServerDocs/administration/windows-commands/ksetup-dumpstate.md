---
title: ksetup dumpstate
description: Ksetup dumpstate 命令参考文章，其中显示了计算机上定义的所有领域的领域设置当前状态。
ms.topic: article
ms.assetid: 3ef2f7b8-97af-4f42-9542-cff324840637
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9c59ad53a7e9d1fb149a0a0a87f5f00938d6a33
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887958"
---
# <a name="ksetup-dumpstate"></a>ksetup dumpstate

显示计算机上定义的所有领域的领域设置的当前状态。 此命令显示与**ksetup**命令相同的输出。

## <a name="syntax"></a>语法

```
ksetup /dumpstate
```

### <a name="remarks"></a>备注

- 此命令的输出包括 (计算机所属域的默认领域) 以及此计算机上定义的所有领域。 每个领域包含以下各项：

  - 所有密钥分发中心 (与此领域关联的 Kdc) 。

  - 此领域的所有**集领域**标志。

  - KDC 密码。

- 此命令不会显示 DNS 检测或命令指定的域名 `ksetup /domain` 。

- 此命令不显示使用命令设置的计算机密码 `ksetup /setcomputerpassword` 。

## <a name="examples"></a>示例

若要在计算机上查找 Kerberos 领域配置，请键入：

```
ksetup /dumpstate
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [ksetup 命令](ksetup.md)