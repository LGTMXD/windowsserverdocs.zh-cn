---
title: 将条件访问根证书部署到本地 AD
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 06/28/2019
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 27a99696f575afa61d3e39aff13fb58cc955936b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818780"
---
# <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>步骤 7.4： 将条件性访问根证书部署到本地 AD

>适用于： Windows Server （半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows 10

在此步骤中，将条件访问根证书部署为本地 AD 的 VPN 身份验证的受信任根证书。

- [**上一个：** 步骤7.3。配置条件访问策略](vpn-config-conditional-access-policy.md)
- [**下一步：** 步骤7.5。创建基于 OMA 的 VPNv2 配置文件到 Windows 10 设备](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. 在 " **VPN 连接**" 页上，选择 "**下载证书**"。

   >[!NOTE]
   >"**下载 base64 证书**" 选项适用于需要用于部署的 base64 证书的某些配置。

2. 使用企业管理员权限登录到已加入域的计算机，并在管理员命令提示符下运行以下命令，将云根证书添加到*Enterprise NTauth*存储中：

   >[!NOTE]
   >对于未加入到 Active Directory 域的 VPN 服务器的环境，必须手动将云根证书添加到_受信任的根证书颁发机构_存储区。

   | Command | 说明 |
   | --- | --- |
   | `certutil -dspublish -f VpnCert.cer RootCA` | 在 " **cn = AIA** " 和 " **Cn = 证书颁发机构**" 容器下创建两个**Microsoft VPN 根 CA 第1代**容器，并发布每个根证书作为**Microsoft vpn 根 ca 第1代**容器的_cACertificate_属性的值。 |
   | `certutil -dspublish -f VpnCert.cer NTAuthCA` | 在 " **cn = AIA** " 和 " **Cn = 证书颁发机构**" 容器下创建一个**cn = NTAuthCertificates**容器，并将每个根证书发布为**CN = NTAuthCertificates**容器的_cACertificate_属性的值。 |
   | `gpupdate /force` | 加速向 Windows server 和客户端计算机添加根证书。 |

3. 验证根证书是否存在于 Enterprise NTauth 存储中并显示为受信任：
   1. 使用已安装**证书颁发机构管理工具**的企业管理员权限登录到服务器。

   >[!NOTE]
   >默认情况下，**证书颁发机构管理工具**已安装证书颁发机构服务器。 它们可以作为服务器管理器中的**角色管理工具**的一部分安装在其他成员服务器上。

   1. 在 VPN 服务器上的 "开始" 菜单中，输入 " **pkiview** " 以打开 "企业 PKI" 对话框。
   1. 在 "开始" 菜单中，输入 " **pkiview** " 以打开 "企业 PKI" 对话框。
   1. 右键单击 "**企业 PKI** "，然后选择 "**管理 AD 容器**"。
   1. 验证每个 Microsoft VPN 根 CA 第1代证书是否存在于下面：
      - NTAuthCertificates
      - AIA 容器
      - 证书颁发机构容器

## <a name="next-steps"></a>后续步骤

[步骤7.5。创建基于 OMA 的 VPNv2 配置文件到 Windows 10 设备](vpn-create-oma-dm-based-vpnv2-profiles.md)：在此步骤中，可以使用 Intune 创建基于 oma 的 VPNv2 配置文件来部署 VPN 设备配置策略。 如果要使用 Microsoft Endpoint Configuration Manager 或 PowerShell 脚本创建 VPNv2 配置文件，请参阅[VPNV2 CSP 设置](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)了解更多详细信息。
