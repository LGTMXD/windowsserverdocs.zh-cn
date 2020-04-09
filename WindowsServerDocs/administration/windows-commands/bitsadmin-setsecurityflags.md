---
title: bitsadmin setsecurityflags
description: 适用于 bitsadmin setsecurityflags 的 Windows 命令主题，用于设置用于确定 BITS 是否应检查证书吊销列表的 HTTP 标志，忽略某些证书错误，并定义服务器重定向 HTTP 请求时要使用的策略。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a7b857bb398e3061a3435a730bf9a751ee2c5e3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849140"
---
# <a name="bitsadmin-setsecurityflags"></a>bitsadmin setsecurityflags

为 HTTP 设置标志，该标志确定 BITS 应检查证书吊销列表、忽略某些证书错误，并定义服务器重定向 HTTP 请求时要使用的策略。 该值是一个无符号整数。

## <a name="syntax"></a>语法

```
bitsadmin /SetSecurityFlags <Job> <Value>
```

### <a name="parameters"></a>参数

|参数|说明|
|---------|-----------|
|作业|该作业的显示名称或 GUID|
|值|请参阅 "备注"|

## <a name="remarks"></a>备注

**Value**参数可以包含以下一个或多个通知标志。

|操作|二进制表示形式|
|------|---------------------|
|启用 CRL 检查|设置最小有效位|
|忽略服务器证书中的公用名无效|从右侧设置第二位|
|忽略服务器证书中的无效日期|从右侧设置第三位|
|忽略服务器证书中的无效证书颁发机构|从右侧设置第4位|
|忽略证书的无效使用|从右侧设置第5位|
|重定向策略|由从右的第9到第11位控制</br>0、0、0-将自动重定向。</br>0，0，1-如果发生重定向，将更新 IBackgroundCopyFile 接口中的远程名称。</br>如果发生重定向，0，1，0位将导致作业失败。|
|允许从 HTTPS 重定向到 HTTP|从右侧设置第12位|

## <a name="examples"></a><a name=BKMK_examples></a>示例

下面的示例设置安全标志，为名为*myJob*的作业启用 CRL 检查。
```
C:\>bitsadmin /SetSecurityFlags myJob 0x0001
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)