---
title: logman 创建 cfg
description: 适用于 * * * * 的 Windows 命令主题
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bfc87093-3ff5-4e19-aa93-d185fb8e2239
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51ae4b64665577aa4795527371764401ce1fe9a1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840880"
---
# <a name="logman-create-cfg"></a>logman 创建 cfg

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

创建配置数据收集器。  

## <a name="syntax"></a>语法  
```  
logman create cfg <[-n] <name>> [options]  
```  
### <a name="parameters"></a>参数  

|                    参数                     |                                                                               说明                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    显示区分上下文的帮助。                                                                     |
|                -s <computer name>                |                                                          在指定的远程计算机上执行命令。                                                          |
|                 -config <value>                  |                                                         指定包含命令选项的设置文件。                                                         |
|                   [-n] <name>                    |                                                                       目标对象的名称。                                                                        |
| -f < bin&#124;bincirc&#124;csv&#124;tsv&#124;sql > |                                                            指定数据收集器的日志格式。                                                             |
|             -[-] u < user [password] >              | 指定要以其身份运行的用户。 输入密码 \* 会生成密码提示。 在密码提示符下键入密码时，不会显示密码。 |
|    -m < [start] [stop] [[start] [stop] [...]]>    |                                                更改为手动启动或停止，而不是计划的开始或结束时间。                                                 |
|                -rf < [[hh：] mm：] ss >                |                                                        在指定的时间段内运行数据收集器。                                                         |
|        -b < M/d/yyyy h:mm： ss [AM&#124;PM] >         |                                                              开始在指定时间收集数据。                                                               |
|        -e < M/d/yyyy h:mm： ss [AM&#124;PM] >         |                                                               在指定的时间结束数据收集。                                                                |
|                -si < [[hh：] mm：] ss >                |                                                 指定性能计数器数据收集器的采样间隔。                                                  |
|              -o < 路径&#124;dsn！日志 >              |                                              指定 SQL 数据库中的输出日志文件或 DSN 和日志集名称。                                               |
|                      -[-] r                       |                                                  每日在指定的开始和结束时间重复数据收集器。                                                  |
|                      -[-] a                       |                                                                     追加到现有日志文件。                                                                     |
|                      -[-] o                      |                                                                     覆盖现有的日志文件。                                                                     |
|           -[-] v < nnnnnn&#124;mmddhhmm >           |                                                   将文件版本信息附加到日志文件名称的末尾。                                                   |
|                  -[-] rc <task>                   |                                                         运行每次关闭日志时指定的命令。                                                          |
|                 -[-] 最大值 <value>                  |                                                 最大日志文件大小（MB）或 SQL 日志的最大记录数。                                                  |
|              -[-] .cnf < [[hh：] mm：] ss >              |     指定 time 后，在指定的时间已过后创建新的文件。 如果未指定时间，则在超出最大大小时创建新文件。     |
|                        -y                        |                                                             在不提示的情况下回答 "是"。                                                              |
|                      -[-] ni                      |                                                         启用（-ni）或禁用（-ni）网络接口查询。                                                          |
|             -reg < 路径 [path [...]]>             |                                                                 指定要收集的注册表值。                                                                 |
|            -"对 < 查询 [查询 [...]]">            |                                                      指定要使用 SQL 查询语言收集的 WMI 对象。                                                       |
|             -ftc < 路径 [path [...]]>             |                                                           指定要收集的文件的完整路径。                                                            |

## <a name="remarks"></a>备注  
其中列出了 [-]，额外-会对选项求反。  
## <a name="examples"></a><a name=BKMK_examples></a>示例  
以下命令使用注册表项 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows NT\Currentverion\\创建名为 cfg_log 的配置数据收集器。  
```  
logman create cfg cfg_log -reg HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\\  
```  
以下命令将创建一个名为 cfg_log 的配置数据收集器，该收集器记录数据库列中 root\wmi 的所有 WMI 对象 MSNdis_Vendordriverversion。  
```  
logman create cfg cfg_log -mgt root\wmi:select * FROM MSNdis_Vendordriverversion  
```  
## <a name="additional-references"></a>其他参考  
[logman](logman.md)  
