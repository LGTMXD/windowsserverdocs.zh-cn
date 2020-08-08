---
title: AD FS 故障排除-循环检测
description: 本文档介绍如何排查循环检测问题
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.openlocfilehash: e3d654f44ba75d9b647c0c1d9db7345c7ea75435
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953087"
---
# <a name="ad-fs-troubleshooting---loop-detection"></a>AD FS 故障排除-循环检测

如果依赖方持续拒绝有效的安全令牌并重定向回 AD FS，则会在 AD FS 中循环。

## <a name="loop-detection-cookie"></a>循环检测 cookie
为了防止发生这种情况，AD FS 实现了所谓的循环检测 cookie。 默认情况下，AD FS 将 cookie 写入名为**MSISLoopDetectionCookie**的 web 被动客户端。 此 cookie 包含时间戳值和多个令牌颁发值。  这允许 AD FS 跟踪客户端在特定时间跨度内访问联合身份验证服务的频率和数量。

如果被动客户端将令牌的联合身份验证服务访问 5 (5) 次，则 AD FS 将引发以下错误：

**MSIS7042：同一客户端浏览器会话已在最后 "" 秒内发出了 " {0} " 个请求 {1} 。请与管理员联系以获取详细信息。**

进入无限循环通常是由不能成功使用 AD FS 颁发的令牌的异常依赖方应用程序引起的，并且该应用程序将被动客户端重新发送回 AD FS （重复）以用于新令牌。  AD FS 将每次向被动客户端发出一个新令牌，前提是它们在20秒内没有超过5次请求。

## <a name="adjusting-the-loop-detection-cookie"></a>调整循环检测 cookie
可以使用 PowerShell 更改令牌颁发值和 timespan 值的数量。

```powershell
Set-AdfsProperties -LoopDetectionMaximumTokensIssuedInterval 5  -LoopDetectionTimeIntervalInSeconds 20
```
**LoopDetectionMaximumTokensIssuedInterval**的最小值为1。

**LoopDetectionTimeIntervalInSeconds**的最小值为5。

执行性能测试时，还可以禁用循环检测。

```powershell
Set-AdfsProperties -EnableLoopDetection $false
```

>[!IMPORTANT]
>不建议永久禁用循环检测，因为这样可以防止用户进入无限循环状态。


## <a name="next-steps"></a>后续步骤

- [AD FS 疑难解答](ad-fs-tshoot-overview.md)



