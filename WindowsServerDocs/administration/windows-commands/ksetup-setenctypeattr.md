---
title: ksetup： setenctypeattr
description: '* * * * 的参考主题'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4cb7380a5fc65734902c6eed0b4b941eda6f6f5a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724563"
---
# <a name="ksetupsetenctypeattr"></a>ksetup： setenctypeattr



设置域的加密类型属性。

## <a name="syntax"></a>语法

```
ksetup /setenctypeattr <Domain name> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

#### <a name="parameters"></a>参数

|参数|描述|
|---------|-----------|
|\<DomainName>|要与之建立连接的域的名称。 使用完全限定的域名或名称的简单格式，如 corp.contoso.com 或 contoso。|
|加密类型|必须是以下受支持的加密类型之一：</br>-DES-CBC-CRC</br>-DES-CBC-MD5</br>-RC4-HMAC-MD5</br>-AES128--HMAC--SHA1-96</br>-AES256--HMAC--SHA1-96|

## <a name="remarks"></a>备注

若要查看 Kerberos 票证授予票证（TGT）的加密类型和会话密钥，请运行**klist**命令并查看输出。

可以通过使用空格将命令中的加密类型隔开，来设置或添加多个加密类型。 不过，每次只能对一个域执行此操作。

如果此命令成功或失败，将显示一条状态消息。

若要设置要连接到并使用的域，请运行**ksetup/Domain \<DomainName>** 命令。

## <a name="examples"></a>示例

确定在此计算机上设置的当前加密类型：
```
klist
```
将域设置为 corp.contoso.com：
```
ksetup /domain corp.contoso.com
```
将域 corp.contoso.com 的 "加密类型" 属性设置为 "AES-256-CTS-HMAC-96-96"：
```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
验证已将 "加密类型" 属性设置为适用于域：
```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>其他参考

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [命令行语法项](command-line-syntax-key.md)