---
title: Vssadmin list shadows
description: Vssadmin list shadows 命令的说明。
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: d3616902fa0b971969e5e906d6dbb200c633d15a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891795"
---
# <a name="vssadmin-list-shadows"></a>Vssadmin list shadows

> 适用于： Windows 10，Windows 8.1，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012，Windows Server 2008 R2，Windows Server 2008

列出指定卷的所有现有卷影副本。 如果使用不带参数的此命令，则会按**卷影副本集**所指示的顺序显示计算机上的所有卷影副本。

## <a name="syntax"></a>语法

```PowerShell
vssadmin list shadows [/for=<ForVolumeSpec>] [/shadow=<ShadowID>]
```

### <a name="parameters"></a>参数

|参数|描述|
|---|---|
|/for =\<ForVolumeSpec>|指定将列出卷影副本的卷。|
|/shadow =\<ShadowID>|列出 ShadowID 指定的卷影副本。 若要获取卷影副本 ID，请使用**vssadmin list shadows**命令。 键入卷影副本 ID 时，请使用以下格式，其中每个*X*表示十六进制字符：<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX （XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX）|

## <a name="additional-references"></a>其他参考

* [命令行语法关键字](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [List](vssadmin.md)
