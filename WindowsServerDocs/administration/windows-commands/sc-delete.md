---
title: Sc delete
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd40b5eb82def3b3c437cbdb5b60d279529d25a0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722194"
---
# <a name="sc-delete"></a>Sc delete



从注册表中删除服务子项。 如果服务正在运行，或者如果另一个进程具有该服务的打开句柄，则该服务将标记为删除。

有关如何使用此命令的示例，请参阅[示例](#examples)。

## <a name="syntax"></a>语法

```
sc [<ServerName>] delete [<ServiceName>]
```

### <a name="parameters"></a>参数

|参数|描述|
|---------|-----------|
|\<ServerName>|指定服务所在的远程服务器的名称。 名称必须使用通用命名约定（UNC）格式（例如， \\ \\myserver）。 若要在本地运行 SC.EXE，请省略此参数。|
|\<ServiceName>|指定**getkeyname**操作返回的服务名称。|
|?|在命令提示符下显示帮助。|

## <a name="remarks"></a>备注

使用 **"控制面板**" 上的 "**添加或删除程序**" 删除 DHCP、DNS 或任何其他内置操作系统服务。 请注意，"**添加或删除程序**" 不仅会删除服务的注册表子项，还会卸载服务并删除其任何快捷方式。

## <a name="examples"></a>示例

若要从本地计算机上的注册表中删除服务子项**NewServ** ，请键入：
```
sc delete newserv
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)