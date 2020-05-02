---
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
title: Fsutil repair
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 1a7931314f7064a62e45d2319e48d58162ab0e11
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725468"
---
# <a name="fsutil-repair"></a>Fsutil repair
> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows 10，Windows Server 2012 R2，Windows 8.1，Windows Server 2012，Windows 8，Windows Server 2008 R2，Windows 7

管理和监视 NTFS 自修复修复操作。



## <a name="syntax"></a>语法

```
fsutil repair [enumerate] <volumepath> [<LogName>]
fsutil repair [initiate] <VolumePath> <FileReference>
fsutil repair [query] <VolumePath>
fsutil repair [set] <VolumePath> <Flags>
fsutil repair [wait][<WaitType>] <VolumePath>

```

### <a name="parameters"></a>参数

|参数|描述|
|-------------|---------------|
|列举|枚举卷损坏日志的条目。|
|\<volumepath>|指定卷作为驱动器名称后跟一个冒号。|
|\<LogName>|$Corrupt-卷中已确认的损坏集。<br />$Verify-卷中一组潜在的未验证损坏。|
|造成|启动 NTFS 自修复。|
|\<FileReference>|指定 NTFS 特定于卷的文件 ID （文件参考编号）。 文件引用包含文件的段号。|
|query|查询 NTFS 卷的自愈状态。|
|set|设置卷的自愈状态。|
|\<标志>|指定设置卷的自愈状态时要使用的修复方法。<p>**Flags**参数可设置为三个值：<p>-   **0x01**：启用常规修复。<br />-   **0x09**：在不修复的情况下警告潜在的数据丢失。<br />-   **0x00**：禁用 NTFS 自修复修复操作。|
|state|查询系统或给定卷的损坏状态。|
|wait|等待修复完成。 如果 NTFS 检测到它在其上执行修复的卷上存在问题，则此选项允许系统等待修复完成，然后再运行挂起的任何脚本。|
|[WaitType {0&#124;1}]|指示是等待当前修复完成，还是等待所有修复完成。 *WaitType*可以设置为以下值：<p>-   **0**：等待所有修复完成。 （默认值）<br />-   **1**：等待当前修复完成。|

## <a name="remarks"></a>备注

-   自愈 NTFS 会尝试联机更正 NTFS 文件系统的损坏，而无需运行**chkdsk.exe** 。 此功能是在 Windows Server 2008 中引入的。 有关详细信息，请参阅[自愈 NTFS](https://go.microsoft.com/fwlink/?LinkID=165401)。

## <a name="examples"></a><a name="BKMK_examples"></a>示例

若要枚举已确认损坏的卷，请键入：

```
fsutil repair enumerate C: $Corrupt 
```

若要启用驱动器 C 上的自愈修复，请键入：

```
fsutil repair set c: 1
```

若要禁用驱动器 C 上的自修复修复，请键入：

```
fsutil repair set c: 0
```

## <a name="additional-references"></a>其他参考
- [命令行语法项](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[自愈 NTFS](https://go.microsoft.com/fwlink/?LinkID=165401)


