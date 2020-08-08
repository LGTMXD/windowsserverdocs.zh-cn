---
title: AD FS 故障排除-声明颁发
description: 本文档介绍如何排查 AD FS 的令牌颁发问题
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: 9eb5ce1ee92e828cc1fd6ceb40ddddec453afe87
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954183"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>AD FS 故障排除-声明颁发
声明是一个使用者对其自身或另一个使用者做出的陈述。  声明由信赖方颁发，它们被赋予一个或多个值，然后打包到 AD FS 服务器颁发的安全令牌。  因为在此过程中有多个移动部件，所以可以将声明颁发分解为这些关键部分。

>[!NOTE]
>你可以使用[ADFS 帮助](https://adfshelp.microsoft.com)站点上的[ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest)来帮助排查声明问题。

## <a name="token-request"></a>令牌请求
转到信赖方时，它会将你重定向到使用令牌请求 AD FS。  请求可能会出现问题。  最有吸引力的功能：

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>请求格式设置为第三方 (特别是 SAML) 

### <a name="pre-formated-urls-that-have-typos"></a>具有拼写错误的预格式化 Url
当使用 Federaion 信赖方颁发令牌时，令牌请求会传入 URL 查询字符串参数。  如果依赖方在执行重定向到 AD FS 时未在该 URL 中指定正确的参数，则可能会导致请求出现问题。


为了验证令牌格式，可以使用 web 调试器工具


## <a name="token-response"></a>令牌响应

## <a name="authentication"></a>Authentication

## <a name="claim-rule-processing"></a>声明规则处理