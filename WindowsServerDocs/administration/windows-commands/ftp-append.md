---
title: ftp 追加
description: Ftp 追加的参考主题
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b53228473b8ea16a0955c244d60fae77cf4f7d7f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725406"
---
# <a name="ftp-append"></a>ftp：追加

> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

使用 "当前文件类型" 设置将本地文件追加到远程计算机上的文件。   
## <a name="syntax"></a>语法  
```  
append <LocalFile> [remoteFile]  
```  
#### <a name="parameters"></a>参数  

|  参数   |                               描述                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     指定要添加的本地文件。                     |
| [remoteFile] | 指定远程计算机<LocalFile>上添加的文件。 |

## <a name="remarks"></a>备注  
如果省略*remoteFile* ，则使用*LocalFile*名称代替远程文件名。  
## <a name="examples"></a>示例  
将 file1 附加到远程计算机上的 file2。  
```  
append file1.txt file2.txt  
```  
将本地 file1 附加到远程计算机上名为 file1 的文件中。  
```  
append file1.txt  
```  
## <a name="additional-references"></a>其他参考  
-   - [命令行语法项](command-line-syntax-key.md)  
