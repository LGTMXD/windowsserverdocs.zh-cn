---
title: add
description: 用于 "**添加**" 的 Windows 命令主题，它将卷添加到要进行卷影复制的卷集中，或将别名添加到别名环境。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9895082cc10223fd08cff6916c20c3af5613e947
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851340"
---
# <a name="add"></a>add

将卷添加到要进行卷影复制的卷集中，或将别名添加到别名环境。 如果在不使用子命令的情况下使用，则**添加**列出当前卷和别名。

> [!NOTE]
> 在创建卷影副本之前，不会将别名添加到别名环境中。 应立即使用 "**添加别名**" 添加所需的别名。

有关如何使用此命令的示例，请参阅[示例](#BKMK_examples)。

## <a name="syntax"></a>语法

```
add 
add volume <Volume> [provider <ProviderID>] 
add alias <AliasName> <AliasValue>
```

## <a name="add-subcommands"></a>添加子命令

| 命令 | 说明 |
| ---------- | ----------- |
| 卷 | 将卷添加到卷影副本集，这是要进行卷影复制的卷集。 有关语法和参数，请参阅[Add volume](add-volume.md) 。 |
| Alias — 别名 | 向别名环境添加给定的名称和值。 请参阅为语法和参数[添加别名](add-alias.md)。 |
| `/?` | 在命令行中显示帮助。 |

## <a name="examples"></a><a name=BKMK_examples></a>示例

若要显示添加的卷和当前在环境中的别名，请键入：

```
add
```

以下输出显示驱动器 C 已添加到卷影副本集：

```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)