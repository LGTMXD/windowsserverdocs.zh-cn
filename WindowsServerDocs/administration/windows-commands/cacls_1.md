---
title: cacls
description: 适用于 cacls 的 Windows 命令主题，用于显示或修改指定文件上的随机访问控制列表（DACL）。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8cc6300563880a587b6544ec8cb61e9010ad6c2c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848240"
---
# <a name="cacls"></a>cacls

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

显示或修改指定文件上的随机访问控制列表（DACL）。  

## <a name="syntax"></a>语法  
```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```  
#### <a name="parameters"></a>参数  

|        参数        |                                                                                            说明                                                                                             |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      \<filename\>       |                                                                            必需。 显示指定文件的 Acl。                                                                             |
|           /t            |                                                          更改当前目录和所有子目录中指定文件的 Acl。                                                          |
|           /m            |                                                                          更改装载到目录的卷的 Acl。                                                                           |
|           /l            |                                                                        处理符号链接本身和目标。                                                                         |
|         /s： sddl         |                                       将 Acl 替换为 SDDL 字符串中指定的 Acl （对于 **/e**、 **/g**、 **/r**、 **/p**或 **/d**无效）。                                        |
|           /e            |                                                                                 编辑 ACL，而不是替换它。                                                                                  |
|           /c            |                                                                                 拒绝访问拒绝错误。                                                                                  |
|    /g user：\<永久状态\>     |   授予指定的用户访问权限。<p>权限的有效值：<p>-n-无<br />-r-读取<br />-w-写入<br />-c-更改（写入）<br />-f-完全控制   |
|      /r user [...]      |                                                                  吊销指定用户的访问权限（仅对 **/e**有效）。                                                                   |
| [/p user：\<永久状态\> [...] | 替换指定用户的访问权限。<p>权限的有效值：<p>-n-无<br />-r-读取<br />-w-写入<br />-c-更改（写入）<br />-f-完全控制 |
|     [/d user [...]      |                                                                                    拒绝指定的用户访问。                                                                                     |
|           /?            |                                                                                在命令提示符下显示帮助。                                                                                |

## <a name="remarks"></a>备注  
- 此命令已弃用。 请改用[icacls](icacls.md) 。  
- 使用下表解释结果：  


  |      Output       |                访问控制项（ACE）适用于                |
  |-------------------|---------------------------------------------------------------------|
  |        OI         |               对象继承。 此文件夹和文件。                |
  |        CI         |           容器继承。 此文件夹和子文件夹。            |
  |        IO         | 仅继承。 ACE 不适用于当前文件/目录。 |
  | 无输出消息 |                          仅限此文件夹。                          |
  |     OICI      |                 此文件夹、子文件夹和文件。                 |
  |   OICI排    |                     仅子文件夹和文件。                      |
  |     CI排      |                          仅子文件夹。                           |
  |     OI排      |                             仅文件。                             |


- 您可以使用通配符（ **？** 和 **\\\*** ）来指定多个文件。  
- 可以指定多个用户。  

## <a name="additional-references"></a>其他参考  
-   - [命令行语法项](command-line-syntax-key.md)   
-   [icacls](icacls.md)  
