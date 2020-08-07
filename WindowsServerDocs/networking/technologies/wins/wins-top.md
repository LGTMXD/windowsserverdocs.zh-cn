---
title: Windows Internet 名称服务 (WINS)
description: 本主题提供有关使 WINS 退役并在网络上使用 DNS 进行名称解析服务的信息。
manager: brianlic
ms.topic: article
ms.assetid: 32eabe7d-1130-4001-a79a-8ddb31993e5b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 36dc2b0e8bbb6b65b0cc3568641017aa51122650
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955494"
---
#  <a name="windows-internet-name-service-wins"></a>Windows Internet 名称服务 (WINS)

>适用于：Windows Server（半年频道）、Windows Server 2016

Windows Internet 名称服务 (WINS) 是传统的计算机名称注册和解析访问服务，该服务将计算机 NetBIOS 名称映射到 IP 地址。

如果你的网络上还没有部署 WINS，请不要部署 WINS，而是部署域名系统 \( DNS \) 。 DNS 还提供计算机名称注册和解析服务，并在 WINS 上包含许多其他权益，如与 Active Directory 域服务的集成。

有关详细信息，请参阅[域名系统 (DNS) ](https://docs.microsoft.com/windows-server/networking/dns/dns-top)

如果已在网络上部署了 WINS，则建议部署 DNS，并使 WINS 停止。
