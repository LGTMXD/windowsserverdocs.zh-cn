---
title: fsutil 脏
description: 适用于 fsutil dirty 命令的参考主题，用于查询或设置卷的未更新位。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: 385a2a7c-d6bd-4f11-9c18-fca0413f9e97
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 72defd974177675f53e89fb8570f028580b7e167
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435862"
---
# <a name="fsutil-dirty"></a>fsutil 脏

> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows 10，Windows Server 2012 R2，Windows 8.1，Windows Server 2012，Windows 8

查询或设置卷的未更新位。 如果设置了卷的未更新位，则在下次重新启动计算机时， **autochk**会自动检查卷中是否存在错误。

## <a name="syntax"></a>语法

```
fsutil dirty {query | set} <volumepath>
```

### <a name="parameters"></a>参数

| 参数 | 说明 |
| --------- | ----------- |
| 查询 | 查询指定卷的已更新位。 |
| set | 设置指定卷的未更新位。 |
| `<volumepath>` | 指定驱动器名称后跟冒号或 GUID，格式如下： `volume{GUID}` 。 |

#### <a name="remarks"></a>备注

- 卷的未更新位表示文件系统可能处于不一致的状态。 可以设置脏位，因为：

    - 卷处于联机状态，它有未完成的更改。

    - 对卷进行了更改，并且计算机在将更改提交到磁盘之前已关闭。

    - 在卷上检测到损坏。

- 如果在计算机重新启动时设置了脏位， **chkdsk**将运行以验证文件系统的完整性，并尝试修复卷的任何问题。

### <a name="examples"></a>示例

若要查询驱动器 C 上的脏位，请键入：

```
fsutil dirty query c:
```

    If the volume is dirty, the following output displays:

    `Volume C: is dirty`

    If the volume isn't dirty, the following output displays:

    `Volume C: is not dirty`

若要设置驱动器 C 上的脏位，请键入：

```
fsutil dirty set C:
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

- [fsutil](fsutil.md)
