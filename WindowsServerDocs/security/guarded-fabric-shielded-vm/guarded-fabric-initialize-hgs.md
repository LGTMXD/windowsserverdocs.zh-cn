---
title: 初始化 HGS
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 42f76dabbe150f229027909f8b58b843f31ae4e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856590"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>初始化主机保护者服务（HGS）

>适用于： Windows Server 2019、Windows Server （半年频道）、Windows Server 2016

初始化 HGS 时，将指定 HGS 用于测量受保护主机的运行状况的模式。 有两个互相排斥的选项。 有关所选模式的背景信息，请参阅[托管商的受保护的构造和受防护的 VM 规划指南](guarded-fabric-planning-for-hosters.md)。

以下主题介绍了每种模式的部署步骤：

- [受 TPM 信任的证明（TPM 模式）](guarded-fabric-initialize-hgs-tpm-mode.md)
- [主机密钥证明（密钥模式）](guarded-fabric-initialize-hgs-key-mode.md)
- [管理员信任的证明（AD 模式）](guarded-fabric-initialize-hgs-ad-mode.md)

应在物理服务器上执行这些步骤。