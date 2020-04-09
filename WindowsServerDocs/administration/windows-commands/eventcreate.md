---
title: eventcreate
description: 适用于 * * * * 的 Windows 命令主题
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2b1b26d-a70e-49a6-832b-91eb5a1a159a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79b10963abef9918e5962fdaf7d387a129873452
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845090"
---
# <a name="eventcreate"></a>eventcreate



使管理员能够在指定的事件日志中创建自定义事件。 有关如何使用此命令的示例，请参阅[示例](#BKMK_examples)。

## <a name="syntax"></a>语法

```
eventcreate [/s <Computer> [/u <Domain\User> [/p <Password>]] {[/l {APPLICATION|SYSTEM}]|[/so <SrcName>]} /t {ERROR|WARNING|INFORMATION|SUCCESSAUDIT|FAILUREAUDIT} /id <EventID> /d <Description>
```

### <a name="parameters"></a>参数

|参数|说明|
|---------|-----------|
|/s \<计算机 >|指定远程计算机的名称或 IP 地址（不使用反斜杠）。 默认值为本地计算机。|
|/u \<Domain\User >|使用 \<用户 > 或 < Domain\User > 指定的用户的帐户权限运行命令。 默认为发出命令的计算机上当前登录用户的权限。|
|/p \<密码 >|指定在 **/u**参数中指定的用户帐户的密码。|
|/l {APPLICATION\|SYSTEM}|指定将在其中创建事件的事件日志的名称。 有效的日志名称为 "应用程序" 和 "系统"。|
|/so \<SrcName >|指定要用于事件的源。 有效的源可以是任何字符串，并且应表示生成事件的应用程序或组件。|
|/t {ERROR\|警告\|信息\|</br>SUCCESSAUDIT\|FAILUREAUDIT}|指定要创建的事件类型。 有效的类型为 ERROR、WARNING、INFORMATION、SUCCESSAUDIT 和 FAILUREAUDIT。|
|/id \<EventID >|指定事件的事件 ID。 有效的 ID 是从1到1000的任何数字。|
|/d \<说明 >|指定要用于新创建的事件的说明。|
|/?|在命令提示符下显示帮助。|

## <a name="remarks"></a>备注

-   不能将自定义事件写入安全日志。

## <a name="examples"></a><a name=BKMK_examples></a>示例

下面的示例演示如何使用 eventcreate 命令：
```
eventcreate /t error /id 100 /l application /d Create event in application log
eventcreate /t information /id 1000 /so winmgmt /d Create event in WinMgmt source
eventcreate /t error /id 2001 /so winword /l application /d new src Winword in application log
eventcreate /s server /t error /id 100 /l application /d Remote machine without user credentials
eventcreate /s server /u user /p password /id 100 /t error /l application /d Remote machine with user credentials
eventcreate /s server1 /s server2 /u user /p password /id 100 /t error /so winmgmt /d Creating events on Multiple remote machines
eventcreate /s server /u user /id 100 /t warning /so winmgmt /d Remote machine with partial user credentials
```

#### <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)
