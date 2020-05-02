---
title: tracerpt
description: 用于分析事件跟踪日志、由性能监视器生成的日志文件和实时事件跟踪提供程序的 tracerpt 参考主题。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb9eaf86-0ef6-4197-b6c8-9cca8a1d723c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79eac1db4d91bfcfe52cf71cbab683b7489d5287
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721315"
---
# <a name="tracerpt"></a>tracerpt

**Tracerpt**命令可用于分析事件跟踪日志、由性能监视器生成的日志文件，以及实时事件跟踪提供程序。 它将生成转储文件、报表文件和报表架构。

## <a name="syntax"></a>语法

```
tracerpt <[-l] <value [value [...]]>|-rt <session_name [session_name [...]]>> [options]
```

## <a name="options"></a>选项

|              选项标志               |                                                                    描述                                                                    |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
|                   -?                   |                                                         显示上下文相关的帮助。                                                          |
|          -config \<filename>           |                                                 加载包含命令选项的设置文件。                                                  |
|                   -y                   |                                                  在不提示的情况下回答 "是"。                                                   |
|            -f \<XML\|HTML>             |                                                                  报表格式。                                                                   |
|         - \<CSV\|.evtx\|XML>          |                                                         转储格式，默认值为 XML。                                                          |
|            -df \<filename>             |                                            创建特定于 Microsoft 的计数/报表架构文件。                                            |
|            -int \<filename>            |                                            将解释的事件结构转储到指定的文件。                                            |
|                  -rts                  |                        报告事件跟踪标头中的原始时间戳。 只能与-o、非报表或-summary 一起使用。                         |
|            -tmf \<filename>            |                                                  指定跟踪消息格式定义文件。                                                  |
|              -tp \<值>              |                            指定 TMF 文件搜索路径。 可以使用多个路径，用分号（;) 分隔。                            |
|              -i \<值>               | 指定提供程序映像路径。 匹配的 PDB 将位于符号服务器中。 可以使用多个路径，用分号（;) 分隔。 |
|             -pdb \<值>              |                             指定符号服务器路径。 可以使用多个路径，用分号（;) 分隔。                             |
|                  -gmt                  |                                              将 WPP 有效负载时间戳转换为格林尼治标准时间。                                               |
|              -rl \<值>              |                                               定义从1到5的系统报告级别。 默认值为 1。                                               |
|          -summary [文件名]           |                                  生成摘要报告文本文件。 如果未指定，则文件名为 summary。                                   |
|             -o [filename]              |                                      生成文本输出文件。 如果未指定，则文件名为 dumpfile。                                      |
|           -report [filename]           |                                  生成文本输出报表文件。 如果未指定，则为 Filename。                                   |
|                  -lr                   |                        指定限制更少。 这对与事件架构不匹配的事件使用最佳做法。                         |
|           -export [文件名]           |                                  生成事件架构导出文件。 如果未指定，则为 "架构"。                                   |
|       [-l]\<值 [值 [...]]>        |                                                   指定要处理的事件跟踪日志文件。                                                    |
| -rt \<session_name [session_name [...]]> |                                                指定实时事件跟踪会话数据源。                                                |

## <a name="examples"></a>示例

- 此示例基于两个事件日志**logfile1**和**logfile2**创建一个报表，并以 xml 格式创建转储文件**logdump。**  
  ```
  tracerpt logfile1.etl logfile2.etl -o logdump.xml -of XML
  ```  
- 此示例创建一个基于事件日志**logfile**的报表，以 xml 格式创建转储文件**logdmp** ，使用最大努力标识不在该架构中的事件，生成一个摘要报表文件**logdump**，并生成报表文件**logrpt**。  
  ```
  tracerpt logfile.etl -o logdmp.xml -of XML -lr -summary logdmp.txt -report logrpt.xml
  ```  
- 此示例使用**logfile1**和**logfile2**这两个事件日志生成包含默认文件名的转储文件和报表文件。  
  ```
  tracerpt logfile1.etl logfile2.etl -o -report
  ```  
- 此示例使用事件日志**logfile .etl**和性能日志**counterfile**来生成报表文件**LOGRPT**和 Microsoft 特定的 xml 架构文件**架构。**  
  ```
  tracerpt logfile.etl counterfile.blg -report logrpt.xml -df schema.xml
  ```  
- 此示例读取实时事件跟踪会话 NT 内核记录器，并以 CSV 格式生成转储文件**logfile。**  
  ```
  tracerpt -rt NT Kernel Logger -o logfile.csv -of CSV
  ```
