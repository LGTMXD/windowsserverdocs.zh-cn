---
title: 使用堡垒林中的 AD 模式初始化 HGS 群集
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 75520c7afe1d3b274e643ab63bbf53159c0e2531
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856690"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-an-existing-bastion-forest"></a>使用现有堡垒林中的 AD 模式初始化 HGS 群集

>适用于：Windows Server（半年频道）、Windows Server 2016


>[!IMPORTANT]
>从 Windows Server 2019 开始，已弃用管理受信任的证明（AD 模式）。 对于不可能进行 TPM 证明的环境，请配置[主机密钥证明](guarded-fabric-initialize-hgs-key-mode-bastion.md)。 主机密钥证明向 AD 模式提供类似的保障，并更易于设置。 

Active Directory 域服务将安装在计算机上，但应保留未配置。

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

继续之前，请确保已为主机保护者服务预留群集对象，并授予已登录的用户对 Active Directory 中的 VCO 和 CNO 对象的**完全控制**权限。
需要将虚拟计算机对象名称传递到 `-HgsServiceName` 参数，并将群集名称传递给 `-ClusterName` 参数。

> [!TIP]
> 请仔细检查 AD 域控制器，确保群集对象已复制到所有 Dc，然后再继续。

如果使用的是基于 PFX 的证书，请在 HGS 服务器上运行以下命令：

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
```

如果你使用的是在本地计算机上安装的证书（例如 HSM 支持的证书和不可导出的证书），请改用 `-SigningCertificateThumbprint` 和 `-EncryptionCertificateThumbprint` 参数。

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [配置结构 DNS](guarded-fabric-configuring-fabric-dns-ad.md)

