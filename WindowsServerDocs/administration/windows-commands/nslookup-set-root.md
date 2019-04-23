---
title: nslookup set root
description: 'Windows 命令主题 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63bdd16263c64f823530119754c31de24e395159
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820788"
---
# <a name="nslookup-set-root"></a>nslookup set root

>适用于：Windows 服务器 （半年频道），Windows Server 2016 中，Windows Server 2012 R2、 Windows Server 2012

更改用于查询根服务器的名称。
## <a name="syntax"></a>语法
```
set root=<RootServer>
```
## <a name="parameters"></a>Parameters
|参数|描述|
|-------|--------|
|<RootServer>|指定根服务器的新名称。 默认值为 ns.nic.ddn.mil。|
|{help &#124; ?}|显示的短摘要**nslookup**子命令。|
## <a name="remarks"></a>备注
-   **集根**子命令会影响**根**子命令。
## <a name="additional-references"></a>其他参考
[命令行语法解答](command-line-syntax-key.md)
[nslookup 根](nslookup-root.md)