---
title: finger
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 907ea637-5c6c-4752-84c2-46bbf2a68a33
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec8040480a7cb75a5a42e051393e3db4a47f8e2f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725615"
---
# <a name="finger"></a>finger

> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

显示有关运行 finger 服务或后台程序的指定远程计算机（通常是运行 UNIX 的计算机）上的用户或用户的信息。 远程计算机指定用户信息显示的格式和输出。 使用不带参数的**指针**会显示帮助。 
## <a name="syntax"></a>语法
```
finger [-l] [<User>] [@<Host>] [...]
```
#### <a name="parameters"></a>参数

| 参数 |                                                                            描述                                                                            |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    -l     |                                                          以长列表格式显示用户信息。                                                           |
|  <User>   | 指定您要了解其信息的用户。 如果省略*User*参数，则**finger**会显示有关指定计算机上的所有用户的信息。 |
|  @<Host>  |        指定运行 finger 服务的远程计算机，在该计算机上查找用户信息。 可以指定计算机名称或 IP 地址。        |
|    /?     |                                                               在命令提示符下显示帮助。                                                                |

## <a name="remarks"></a>备注
可以User@Host指定多个参数。
必须使用连字符（-）而不是斜线（/）作为**finger**参数的前缀。
仅当 Internet 协议（TCP/IP）协议安装为网络连接中的网络适配器属性中的组件时，此命令才可用。
Windows Server 2003 不提供 finger 服务。
## <a name="examples"></a>示例
若要在计算机 users.microsoft.com 上显示 user1 的信息，请键入：
```
finger user1@users.microsoft.com
```
若要显示计算机 users.microsoft.com 上所有用户的信息，请键入：
```
finger @users.microsoft.com
```
## <a name="additional-references"></a>其他参考
-   - [命令行语法项](command-line-syntax-key.md)
