---
title: 创建主机密钥并将其添加到 HGS
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 4572c6424f018d711a18d5ee763b00a253a73529
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961601"
---
# <a name="create-a-host-key-and-add-it-to-hgs"></a>创建主机密钥并将其添加到 HGS

>适用于：Windows Server 2019

本主题介绍了如何使用主机密钥证明 (密钥模式) 将 Hyper-v 主机准备成为受保护的主机。 你将创建一个主机密钥对 (或使用现有证书) 并将该密钥的公共一半添加到 HGS。

## <a name="create-a-host-key"></a>创建主机密钥

1. 在 Hyper-v 主机计算机上安装 Windows Server 2019。
2. 安装 Hyper-v 和主机保护者 Hyper-v 支持功能：

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

3. 自动生成主机密钥，或选择现有证书。 如果你使用的是自定义证书，则它应至少具有一个2048位的 RSA 密钥、客户端身份验证 EKU 和数字签名密钥用法。

    ```powershell
    Set-HgsClientHostKey
    ```

    或者，如果想要使用自己的证书，也可以指定指纹。
    如果要在多台计算机上共享证书，或者使用绑定到 TPM 或 HSM 的证书，这会很有用。 下面是创建与 TPM 绑定的证书 (的示例，该证书可防止其在另一台计算机上盗取并使用私钥，只需要 TPM 1.2) ：

    ```powershell
    $tpmBoundCert = New-SelfSignedCertificate -Subject "Host Key Attestation ($env:computername)" -Provider "Microsoft Platform Crypto Provider"
    Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
    ```

4. 获取密钥的公共一半以提供给 HGS 服务器。 你可以使用以下 cmdlet，或者，如果你的证书存储在其他位置，请提供包含密钥公共一半的 .cer。 请注意，我们只是在 HGS 上存储和验证公钥;我们不会保留任何证书信息，也不会验证证书链或到期日期。

    ```powershell
    Get-HgsClientHostKey -Path "C:\temp\$env:hostname-HostKey.cer"
    ```

5. 将 .cer 文件复制到 HGS 服务器。

## <a name="add-the-host-key-to-the-attestation-service"></a>将主机密钥添加到证明服务

此步骤在 HGS 服务器上完成，并允许主机运行受防护的 Vm。 建议将名称设置为主机的 FQDN 或资源标识符，以便可以轻松地引用安装了该密钥的主机。

```powershell
Add-HgsAttestationHostKey -Name MyHost01 -Path "C:\temp\MyHost01-HostKey.cer"
```

## <a name="next-step"></a>后续步骤

- [确认主机可成功证明](guarded-fabric-confirm-hosts-can-attest-successfully.md)

## <a name="additional-references"></a>其他参考

- [为受保护的主机和受防护的 VM 部署主机保护者服务](guarded-fabric-deploying-hgs-overview.md)
