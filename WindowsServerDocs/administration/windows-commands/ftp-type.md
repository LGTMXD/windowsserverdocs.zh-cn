---
title: ftp 类型
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e96dcd4-08f8-4e7b-90b7-1e1761fea4c7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5531da30118914599ed0f85bfd10bd02ae89ffcf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725080"
---
# <a name="ftp-type"></a>ftp：类型

> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

设置或显示文件传输类型。   
## <a name="syntax"></a>语法  
```  
type [<typeName>]  
```  
#### <a name="parameters"></a>参数  

|  参数   |            描述            |
|--------------|-----------------------------------|
| [<typeName>] | 指定文件传输类型。 |

## <a name="remarks"></a>备注  
- 如果未指定*typeName* ，则显示当前类型。  
- **ftp**支持两种文件传输类型： ASCII 和二进制。  
  默认文件传输类型为 ASCII。  传输文本文件时应使用**ascii**命令。 在 ASCII 模式下，执行与网络标准字符集之间的字符转换。 例如，行尾字符根据需要根据目标上的操作系统进行转换。  
  传输可执行文件时应使用**二进制**命令。 在二进制模式下，文件以单字节单位移动。  
  ## <a name="examples"></a>示例  
  将 "文件传输类型" 设置为 "ASCII"。  
  ```  
  type ascii  
  ```  
  将 "传输文件类型" 设置为 "二进制"。  
  ```  
  type binary  
  ```  
  ## <a name="additional-references"></a>其他参考  
- - [命令行语法项](command-line-syntax-key.md)  
