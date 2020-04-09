---
title: TLS/SSL 概述（Schannel SSP）
description: Windows Server 安全
ms.prod: windows-server
ms.technology: security-tls-ssl
ms.topic: article
ms.assetid: 1b7b0432-1bef-4912-8c9a-8989d47a4da9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/16/2018
ms.openlocfilehash: e0045edf1d04feabac2354d47132b86e6d27ad2d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853620"
---
# <a name="tlsssl-overview-schannel-ssp"></a>TLS/SSL 概述（Schannel SSP）

>适用于: Windows Server (半年频道)、Windows Server 2016、Windows 10

适用于 IT 专业人员的本主题介绍了使用 Schannel 安全服务提供程序（SSP）在 Windows 中实现的 TLS 和 SSL 实现，具体方法是：描述实际应用程序、Microsoft 实现中的更改和软件要求，以及 Windows Server 2012 和 Windows 8 的其他资源。

## <a name="description"></a><a name="BKMK_OVER"></a>2008
Schannel 是安全支持提供程序 (SSP)，可实现安全套接字层 (SSL) 和传输层安全 (TLS) Internet 标准身份验证协议。

安全支持提供程序接口 (SSPI) 是 Windows 系统用于执行安全相关功能（包括身份验证）的 API。 SSPI 充当多个 Ssp （包括 Schannel SSP）的通用接口。

TLS 版本1.0、1.1 和1.2、SSL 版本2.0 和3.0、数据报传输层安全性 \(DTLS\) 协议版本1.0 和专用通信传输 \(PCT\) 协议基于公钥加密。 Schannel 身份验证协议套件提供这些协议。 所有 Schannel 协议均使用客户端/服务器模型。

## <a name="applications"></a><a name="BKMK_APP"></a>应用程序
管理网络时的一个问题是保护跨未受信任的网络在应用程序之间发送的数据的安全。 你可以使用 TLS 和 SSL 对服务器和客户端计算机进行身份验证，然后使用协议对经过身份验证的参与方之间的消息进行加密。

例如，你可以将 TLS/SSL 用于：

-   电子商务网站受 SSL 保护的交易
-   对受 SSL 保护的网站的经身份验证的客户端访问
-   远程访问
-   SQL 访问
-   E-mail

## <a name="requirements"></a><a name="BKMK_SOFT"></a>要求
TLS 和 SSL 协议使用客户端/服务器模型，且基于需要公钥基础结构的证书身份验证。

## <a name="server-manager-information"></a><a name="BKMK_INSTALL"></a>服务器管理器信息
无需执行任何配置步骤即可实现 TLS、SSL 或 Schannel。

## <a name="see-also"></a>另请参阅 ##

-   [Schannel 安全包](https://docs.microsoft.com/windows/desktop/com/schannel)
-   [安全通道](https://docs.microsoft.com/windows/desktop/SecAuthN/secure-channel)
-   [传输层安全协议](https://docs.microsoft.com/windows/desktop/SecAuthN/transport-layer-security-protocol)
