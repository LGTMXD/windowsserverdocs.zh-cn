---
title: ksetup： delkdc
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7d6ec389-094c-4a7b-a78b-605497ddc289
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 19ebe322d414d1ae9007275772ccd747f6f0ff8d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724661"
---
# <a name="ksetupdelkdc"></a>ksetup： delkdc



删除 Kerberos 领域密钥发行中心（KDC）名称的实例。

## <a name="syntax"></a>语法

```
ksetup /delkdc <RealmName> <KDCName>
```

#### <a name="parameters"></a>参数

|参数|描述|
|---------|-----------|
|\<RealmName>|领域名称被声明为大写的 DNS 名称，例如 CORP。CONTOSO.COM，在**ksetup**运行时，它将作为默认领域列出。 这是你尝试删除其他 KDC 的领域。|
|\<KDCName>|KDC 名称被声明为不区分大小写的完全限定的域名，如 mitkdc.contoso.com。|

## <a name="remarks"></a>备注

这些映射存储在注册表的**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains**中。 若要从多台计算机中删除领域配置数据，请使用安全配置模板管理单元和策略分发，而不是在单独的计算机上显式使用**ksetup** 。

在运行 Windows 2000 Server Service Pack 1 （SP1）和更早版本的计算机上，必须重新启动计算机，然后才能使用更改的领域设置配置。

若要验证计算机的默认领域名称，或者要验证此命令是否按预期运行，请在命令提示符下运行**ksetup** ，并验证列表中是否不存在已删除的 KDC。

## <a name="examples"></a>示例

此计算机的安全要求已更改，因此必须删除 Windows 领域和非 Windows 领域之间的链接。 首先，确定要删除的关联，并生成现有关联的输出：
```
ksetup
```
使用以下命令删除关联：
```
Ksetup /delkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

## <a name="additional-references"></a>其他参考

-   [Ksetup](ksetup.md)
-   - [命令行语法项](command-line-syntax-key.md)