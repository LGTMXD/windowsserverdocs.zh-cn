---
title: 使用 AllDriverPackages 子命令
description: AllDriverPackages 的参考主题，用于将文件夹中存储的所有驱动程序包添加到服务器。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 31daa8fc3e3304dba5079672ea4619fd085dd74f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721161"
---
# <a name="add-alldriverpackages"></a>AllDriverPackages

将文件夹中存储的所有驱动程序包添加到服务器。

## <a name="syntax"></a>语法

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

### <a name="parameters"></a>参数

|          参数           |                                                              描述                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|  /FolderPath：\<文件夹路径>  |                      指定包含驱动程序包 .inf 文件的文件夹的完整路径。                      |
|   [/Server：\<Server name>]   | 指定服务器的名称。 此名称可以是 NetBIOS 名称或 FQDN。 如果未指定服务器名称，则使用本地服务器。 |
|     [/Architecture： {x86      |                                                                 ia64                                                                  |
| [/DriverGroup：\<组名称>] |                             指定应将包添加到其中的驱动程序组的名称。                             |

## <a name="examples"></a>示例

若要添加驱动程序包，请键入下列内容之一：
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers\Printers /DriverGroup:Printer Drivers
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)

[WdsDriverPackage](https://technet.microsoft.com/library/dn283440.aspx)