---
title: bootcfg rmsw
description: 适用于 bootcfg rmsw 的 Windows 命令主题，它删除指定操作系统项的操作系统加载选项。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fd7e4248-880e-4e2b-929e-87f8d44b9a63
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 956732f396e0fa353a8acd55953e46605a5c4200
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848440"
---
# <a name="bootcfg-rmsw"></a>bootcfg rmsw

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

删除指定操作系统项的操作系统加载选项。

## <a name="syntax"></a>语法
```
bootcfg /rmsw [/s <computer> [/u <Domain>\<User> [/p <Password>]]] [/mm] [/bv] [/so] [/ng] /id <OSEntryLineNum>
```
### <a name="parameters"></a>参数

|      参数       |                                                                                                      说明                                                                                                       |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                                   指定远程计算机的名称或 IP 地址（不使用反斜杠）。 默认值为本地计算机。                                                   |
| /u <Domain>\\<User>  |          使用 <User> 或 <Domain>\\<User>指定的用户的帐户权限运行命令。 默认为发出命令的计算机上当前登录用户的权限。          |
|    /p <Password>     |                                                                 指定在 **/u**参数中指定的用户帐户的密码。                                                                  |
|         /mm          |           从指定的 <OSEntryLineNum>中移除/maxmem 选项及其关联的最大内存值。 /Maxmem 选项指定操作系统可使用的最大 RAM 量。            |
|         /bv          |                     从指定的 <OSEntryLineNum>中移除/basevideo 选项。 /Basevideo 选项指示操作系统使用已安装视频驱动程序的标准 VGA 模式。                     |
|         /so          |                         从指定的 <OSEntryLineNum>中删除/sos 选项。 /Sos 选项指示操作系统在加载时显示设备驱动程序名称。                          |
|         /ng          |                         从指定的 <OSEntryLineNum>中移除/noguiboot 选项。 /Noguiboot 选项禁用出现在 CTRL + ALT + del logon 提示符之前的进度栏。                          |
| /id <OSEntryLineNum> | 在从中删除 OS 加载选项的 Boot.ini 文件的 "[操作系统]" 部分中指定操作系统条目行号。 [操作系统] 部分标题后面的第一行是1。 |
|          /?          |                                                                                          在命令提示符下显示帮助。                                                                                          |

## <a name="examples"></a><a name=BKMK_examples></a>示例
下面的示例演示如何使用**bootcfg/rmsw**命令：
```
bootcfg /rmsw /mm 64 /id 2 
bootcfg /rmsw /so /id 3 
bootcfg /rmsw /so /ng /s srvmain /u hiropln /id 2 
bootcfg /rmsw /ng /id 2 
bootcfg /rmsw /mm 96 /ng /s srvmain /u maindom\hiropln /p p@ssW23 /id 2       
```
## <a name="additional-references"></a>其他参考
- [命令行语法项](command-line-syntax-key.md)
