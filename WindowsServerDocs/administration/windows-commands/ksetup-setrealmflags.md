---
title: ksetup： setrealmflags
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bcb2824e-fba7-4ebe-be62-e62b4fae5b17
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a32ea03f4f0e76f03c7a0b505563e6bcf972b80
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724573"
---
# <a name="ksetupsetrealmflags"></a>ksetup： setrealmflags



设置指定领域的领域标志。

## <a name="syntax"></a>语法

```
ksetup /setrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

#### <a name="parameters"></a>参数

|参数|描述|
|---------|-----------|
|\<RealmName>|领域名称被声明为大写的 DNS 名称，例如 CORP。CONTOSO.COM。|
|领域标志|表示下列标志之一：</br>-SendAddress</br>- TcpSupported</br>-委托</br>- NcSupported</br>-RC4|

## <a name="remarks"></a>备注

领域标志指定了不基于 Windows Server 操作系统的 Kerberos 领域的其他功能。 运行 Windows Server 2003、Windows Server 2008 或 Windows Server 2008 R2 的计算机可以使用 Kerberos 服务器来管理身份验证，而不是使用运行 Windows Server 操作系统的域，这些系统参与了 Kerberos 领域。 此条目将建立领域的功能。 下表对每个进行了说明。

|值|领域标志|描述|
|-----|----------|-----------|
|0xF|全部|设置所有领域标志。|
|0x00|无|未设置领域标志，并且未启用任何其他功能。|
|0x01|SendAddress|此 IP 地址将包含在票证授予票证中。|
|0x02|TcpSupported|此领域支持传输控制协议（TCP）和用户数据报协议（UDP）。|
|0x04|委托|此领域中的每个人都受信任，可用于委派。|
|0x08|NcSupported|此领域支持名称规范化，这允许 DNS 和领域的命名标准。|
|0x80|RC4|此领域支持 RC4 加密以启用跨领域信任，这允许使用 TLS。|

领域标志存储在注册表的**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\**<em>RealmName</em>中。 默认情况下，注册表中不存在此项。 可以使用[Ksetup： addrealmflags](ksetup-addrealmflags.md)命令填充注册表。

可以通过查看**ksetup**的输出来查看哪些领域标志可用和设置。

## <a name="examples"></a>示例

列出可用的和设置领域 CONTOSO 的领域标志：
```
ksetup
```
设置当前未设置的两个标志：
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
运行**ksetup**命令，以验证是否已通过查看输出和查找**领域**标志来设置领域标志。

## <a name="additional-references"></a>其他参考

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   - [命令行语法项](command-line-syntax-key.md)