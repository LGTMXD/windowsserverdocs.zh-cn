---
title: 网络控制器的部署后步骤
description: 本主题为 Windows Server 2016 Datacenter 中的网络控制器的非 Kerberos 部署提供证书配置说明。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: eea0aca9-8d89-48fb-8068-fca40c90d34b
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: bb43de904be7a811083e71edce9421a236f20a27
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859630"
---
# <a name="post-deployment-steps-for-network-controller"></a>网络控制器的部署后步骤

安装网络控制器时，可以选择 Kerberos 或非 Kerberos 部署。

对于非\-Kerberos 部署，你必须配置证书。

## <a name="configure-certificates-for-non-kerberos-deployments"></a>为非 Kerberos 部署配置证书

如果网络控制器 \(Vm\) 的计算机或虚拟机未加入域\-，则必须通过完成以下步骤来配置基于证书的身份验证\-。

- 在网络控制器上创建用于计算机身份验证的证书。 证书使用者名称必须与网络控制器计算机或 VM 的 DNS 名称相同。

- 在管理客户端上创建证书。 此证书必须受网络控制器信任。
  
- 在网络控制器计算机或 VM 上注册证书。 证书必须满足以下要求。
  
    -  服务器身份验证和客户端身份验证目的都必须在增强型密钥用法 \(EKU\) 或应用程序策略扩展中进行配置。 服务器身份验证的对象标识符为1.3.6.1.5.5.7.3.1。 客户端身份验证的对象标识符为1.3.6.1.5.5.7.3.2。
  
    - 证书使用者名称应解析为：
  
        - 网络控制器计算机或 VM 的 IP 地址（如果在单台计算机或 VM 上部署了网络控制器）。

        - 如果在多台计算机上部署了网络控制器和/或多个 Vm，则 REST IP 地址。
  
    - 此证书必须受所有 REST 客户端信任。 证书还必须受软件负载平衡（SLB）复用器（MUX）和网络控制器管理的 southbound 主机计算机的信任。
  
    - 证书可以由证书颁发机构（CA）注册，也可以是自签名证书。 不建议将自签名证书用于生产部署，但对于测试实验室环境是可接受的。
  
    - 必须在所有网络控制器节点上设置相同的证书。 在一个节点上创建证书之后，可以导出该证书（包含私钥），并将其导入其他节点。

有关详细信息，请参阅[网络控制器](Network-Controller.md)。
