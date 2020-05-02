---
title: ksetup： listrealmflags
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa96e4da-6b98-4c05-bccf-73cbf33258c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0646be8daaad4bc3303389cfca1f3a09136fe1a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724619"
---
# <a name="ksetuplistrealmflags"></a>ksetup： listrealmflags



列出**ksetup**可以报告的可用领域标志。

## <a name="syntax"></a>语法

```
ksetup /listrealmflags
```

#### <a name="parameters"></a>参数

无

## <a name="remarks"></a>备注

领域标志指定非基于 Windows 的 Kerberos 领域的其他功能。 运行 Windows Server 2003、Windows Server 2008 或 Windows Server 2008 R2 的计算机可以使用基于非 Windows 的 Kerberos 服务器来管理身份验证，而不是使用运行 Windows Server 操作系统的域。 这些系统参与 Kerberos 领域，而不是 Windows 域。 此条目将建立领域的功能。 下表对每个进行了说明。

|值|领域标志|描述|
|-----|----------|-----------|
|0xF|全部|设置所有领域标志。|
|0x00|无|未设置领域标志，并且未启用任何其他功能。|
|0x01|SendAddress|此 IP 地址将包含在票证授予票证中。|
|0x02|TcpSupported|此领域支持传输控制协议（TCP）和用户数据报协议（UDP）。|
|0x04|委托|此领域中的每个人都受信任，可用于委派。|
|0x08|NcSupported|此领域支持名称规范化，这允许 DNS 和领域的命名标准。|
|0x80|RC4|此领域支持 RC4 加密以启用跨领域信任，这允许使用 TLS。|

领域标志存储在注册表中， **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\**的<em>领域名称</em>。 默认情况下，注册表中不存在此项。 可以使用[Ksetup： addrealmflags](ksetup-addrealmflags.md)命令填充注册表。

## <a name="examples"></a>示例

列出此计算机上的已知领域标志：
```
ksetup /listrealmflags
```
通过在命令行中键入以下命令之一，设置**Ksetup**不知道的可用领域标志：
```
ksetup /setrealmflags CORP.CONTOSO.COM sendaddress tcpsupported delete ncsupported
```
```
ksetup /setrealmflags CORP.CONTOSO.COM 0xF
```

## <a name="additional-references"></a>其他参考

-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [Ksetup](ksetup.md)
-   - [命令行语法项](command-line-syntax-key.md)