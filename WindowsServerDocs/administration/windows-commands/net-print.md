---
title: Net print
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a2fa74da638c23c071e86c19d73cea35c52e8516
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723811"
---
# <a name="net-print"></a>Net print

> 适用于： Windows Server （半年频道），Windows Server 2019，Windows Server 2016，Windows Server 2012 R2，Windows Server 2012

显示有关指定打印机队列或指定的打印作业的信息，或控制指定的打印作业。
> [!NOTE]
> 此命令已在 Windows 7 和 Windows Server 2008 R2 中弃用。 但是，可以使用 prnjobs、Windows Management Instrumentation （WMI）或 Windows PowerShell cmdlet 执行许多相同的任务。 有关详细信息，请[参阅 prnjobs](prnjobs.md)、 [Windows Management Instrumentation](https://go.microsoft.com/fwlink/?LinkID=29991) https://go.microsoft.com/fwlink/?LinkID=29991)（、 [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=128426) （https://go.microsoft.com/fwlink/?LinkID=128426)和[TechNet 脚本中心库](https://go.microsoft.com/fwlink/?LinkId=164635)（https://go.microsoft.com/fwlink/?LinkId=164635)）。
> ## <a name="syntax"></a>语法
> ```
> Net print {\\<computerName>\<Sharename> | 
> \\<computerName> <JobNumber> [/hold | /release | /delete]} [help]
> ```
> ### <a name="parameters"></a>参数
> 
> |               参数               |                                                                                                                                                                                                                     描述                                                                                                                                                                                                                      |
> |----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |    \\\\<computerName>\\<Sharename>     |                                                                                                                                                                            按名称指定要显示其信息的计算机和打印队列。                                                                                                                                                                             |
> |           \\\\<computerName>           |                                                                                                                                 指定（按名称）承载要控制的打印作业的计算机。 如果未指定计算机，则假定为本地计算机。 需要<JobNumber>参数。                                                                                                                                  |
> |              <JobNumber>               |                                             指定要控制的打印作业的编号。 此编号由承载打印作业的打印队列的计算机分配。 计算机将编号分配给打印作业后，该数字不会分配给该计算机所承载的任何队列中的任何其他打印作业。 使用参数时是\\ \\ <computerName>必需的。                                             |
> | [/hold &#124;/release &#124;/delete] | 指定要对打印作业执行的操作。<p>- **/Hold**参数将延迟作业，允许其他打印作业绕过它。<br />- **/Release**参数将释放已延迟的打印作业。<br />- **/Delete**参数从打印队列中删除打印作业。<p>如果指定了作业编号，但未指定任何操作，则会显示有关打印作业的信息。 |
> |                  帮助                  |                                                                                                                                                                                                     显示**Net print**命令的帮助。                                                                                                                                                                                                     |
> 
> ## <a name="remarks"></a>备注
> - **Net** \\ \\ print <computerName>显示有关共享打印机队列中打印作业的信息。 下面的示例显示了名为激光器的共享打印机的队列中所有打印作业的报表：
>   ```
>   printers at \\PRODUCTION
>   Name              Job #      Size      Status
>   -----------------------------
>   LASER Queue       3 jobs               *printer active*
>      USER1          84        93844      printing
>      USER2          85        12555      Waiting
>      USER3          86        10222      Waiting
>   ```
> - 下面是打印作业报表的示例：
>   ```
>   Job #            35
>   Status           Waiting
>   Size             3096
>   remark
>   Submitting user  USER2
>   Notify           USER2
>   Job data type
>   Job parameters
>   additional info
>   ```
>   ## <a name="examples"></a>示例
>   此示例演示如何在\\\Production 计算机上列出 Dotmatrix 打印队列的内容：
>   ```
>   Net print \\Production\Dotmatrix 
>   ```
>   此示例显示了如何在\\\Production 计算机上显示有关作业编号35的信息：
>   ```
>   Net print \\Production 35 
>   ```
>   此示例演示如何在\\\Production 计算机上延迟作业编号263：
>   ```
>   Net print \\Production 263 /hold 
>   ```
>   此示例演示如何在\\\Production 计算机上发布作业编号263：
>   ```
>   Net print \\Production 263 /release 
>   ```
>   ## <a name="additional-references"></a>其他参考
>   - [命令行语法密钥](command-line-syntax-key.md)
>   [打印命令参考](print-command-reference.md)
