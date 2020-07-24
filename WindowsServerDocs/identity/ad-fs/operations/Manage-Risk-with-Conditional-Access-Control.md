---
ms.assetid: a0f7bb11-47a5-47ff-a70c-9e6353382b39
title: 使用条件访问控制管理风险
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b72f324d7037df30a9a8b1f0b9a966a633d30950
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966489"
---
# <a name="manage-risk-with-conditional-access-control"></a>使用条件访问控制管理风险




-   [关键概念-AD FS 中的条件访问控制](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [使用条件访问控制管理风险](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

## <a name="key-concepts---conditional-access-control-in-ad-fs"></a><a name="BKMK_1"></a>关键概念 — AD FS 中的条件访问控制
AD FS 的总体功能是颁发一个包含声明集的访问令牌。 有关 AD FS 接受的声明，然后发出问题的决策由声明规则控制。

AD FS 中的访问控制是使用颁发授权声明规则实施的，这些规则用于发出允许或拒绝声明，这些声明将确定是否允许某个用户或用户组访问 AD FS 保护的资源。 只能在信赖方信任上设置授权规则。

|规则选项|规则逻辑|
|---------------|--------------|
|允许所有用户|如果传入声明类型等于*任何声明类型*并且值等于*任何值*，则发出值等于 *“允许”* 的声明|
|允许具有此传入声明的用户访问|如果传入声明类型等于*指定的声明类型*并且值等于*指定的声明值*，则发出值等于 *“允许”* 的声明|
|拒绝具有此传入声明的用户访问|如果传入声明类型等于*指定的声明类型*并且值等于*指定的声明值*，则发出值等于 *“拒绝”* 的声明|

有关这些规则选项和逻辑的详细信息，请参阅[何时使用授权声明规则](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913560(v=ws.11))。

在 Windows Server 2012 R2 的 AD FS 中，使用多种因素（包括用户、设备、位置和身份验证数据）增强了访问控制。 这是通过提高授权声明规则所用的声明类型的多样性来实现的。  换句话说，在 Windows Server 2012 R2 的 AD FS 中，你可以基于用户标识或组成员身份、网络位置、设备（它是否已加入工作区）强制实施条件性访问控制。有关详细信息，请参阅[从任何设备加入工作区以实现 SSO 和无缝第二重身份验证](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)，以及身份验证状态（是否执行多重身份验证（MFA））。

Windows Server 2012 R2 的 AD FS 中的条件访问控制具有以下优势：

-   灵活、明确的按应用程序授权策略，凭此可以基于用户、设备、网络位置和身份验证状态允许或拒绝访问

-   为信赖方应用程序创建颁发授权规则

-   针对常见的条件访问控制方案提供丰富的 UI 体验

-   针对高级条件访问控制方案提供丰富的声明语言和 Windows PowerShell 支持

-   自定义（按信赖方应用程序） "拒绝访问" 消息。 有关详细信息，请参阅[自定义 AD FS 登录页](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280950(v=ws.11))。 由于能够自定义这些消息，你可以解释为何用户被拒绝访问，并尽可能协助进行自助式补救，例如，提示用户将其设备加入工作区。 有关详细信息，请参阅 [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)。

下表包括 Windows Server 2012 R2 中 AD FS 可用来实现条件访问控制的所有声明类型。

|声明类型|说明|
|--------------|---------------|
|电子邮件地址|用户的电子邮件地址。|
|名|用户的给定名称。|
|名称|用户的唯一名称。|
|UPN|用户的用户主体名称 (UPN)。|
|公用名|用户的公用名。|
|AD FS 1.x 电子邮件地址|与 AD FS 1.1 或 AD FS 1.0 互操作时使用的用户电子邮件地址。|
|Group|用户所属的组。|
|AD FS 1.x UPN|与 AD FS 1.1 或 AD FS 1.0 互操作时使用的用户 UPN。|
|角色|用户具有的角色。|
|Surname|用户的姓氏。|
|PPID|用户的专用标识符。|
|名称 ID|用户的 SAML 名称标识符。|
|身份验证时间戳|用于显示用户进行身份验证的日期和时间。|
|身份验证方法|对用户进行身份验证时使用的方法。|
|“仅拒绝”组 SID|用户的“仅拒绝”组 SID。|
|“仅拒绝”主 SID|用户的“仅拒绝”主 SID。|
|“仅拒绝”主组 SID|用户的“仅拒绝”主组 SID。|
|组 SID|用户的组 SID。|
|主组 SID|用户的主组 SID。|
|主 SID|用户的主 SID。|
|Windows 帐户名|用户的域帐户名，格式为“域\用户”。|
|为注册用户|用户已注册，可以使用此设备。|
|设备标识符|设备的标识符。|
|Device Registration 标识符|Device Registration 的标识符。|
|Device Registration 显示名称|Device Registration 的显示名称。|
|设备 OS 类型|设备的操作系统类型。|
|设备 OS 版本|设备的操作系统版本。|
|为托管设备|设备由管理服务管理。|
|转发的客户端 IP|用户的 IP 地址。|
|客户端应用程序|客户端应用程序的类型。|
|客户端用户代理|客户端访问应用程序时使用的设备类型。|
|客户端 IP|客户端的 IP 地址。|
|终结点路径|终结点绝对路径，可用于确定主动客户端与被动客户端。|
|代理|传递请求的联合服务器代理的 DNS 名称。|
|应用程序标识符|信赖方的标识符。|
|应用程序策略|证书的应用程序策略。|
|授权密钥标识符|为已颁发证书签名的证书的授权密钥标识符扩展。|
|基本约束|证书的基本约束之一。|
|增强型密钥用法|描述证书的增强密钥用法之一。|
|颁发者|颁发此 X.509 证书的证书颁发机构的名称。|
|颁发者名称|证书颁发者的可分辨名称。|
|密钥用法|证书的密钥用法之一。|
|不晚于|以本地时间表示的证书有效截止日期。|
|不早于|以本地时间表示的证书生效日期。|
|证书策略|颁发证书所依据的策略。|
|公钥|证书的公钥。|
|证书原始数据|证书的原始数据。|
|使用者可选名称|证书的备用名称之一。|
|序列号|证书的序列号。|
|签名算法|用于创建证书签名的算法。|
|主题|证书中的使用者。|
|使用者密钥标识符|证书的使用者密钥标识符。|
|使用者名称|证书中的使用者可分辨名称。|
|V2 模板名称|颁发或续订证书时使用的版本 2 证书模板的名称。 这是一个特定于 Microsoft 的值。|
|V1 模板名称|颁发或续订证书时使用的版本 1 证书模板的名称。 这是一个特定于 Microsoft 的值。|
|Thumbprint|证书的指纹。|
|X.509 版本|证书的 X.509 格式版本。|
|企业网络内部|用于指明请求是否从公司网络中发出。|
|密码过期时间|用于显示密码到期时间。|
|密码到期天数|用于显示距密码到期的天数。|
|更新密码 URL|用于显示更新密码服务的 Web 地址。|
|身份验证方法引用|用于指示用户身份验证所用的所有身份验证方法。|

## <a name="managing-risk-with-conditional-access-control"></a><a name="BKMK_2"></a>使用条件访问控制管理风险
你可以使用提供的设置，通过实施条件访问控制以多种方法来管理风险。

### <a name="common-scenarios"></a>常见方案
例如，假设有一个简单的方案，该方案基于用户的特定应用程序的组成员身份数据（信赖方信任）实施条件访问控制。 换句话说，你可以在联合服务器上设置一个颁发授权规则，以允许属于 AD 域中特定组的用户访问受 AD FS 保护的特定应用程序。  [Walkthrough Guide: Manage Risk with Conditional Access Control](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)中介绍了有关实施此方案的详细分步说明（使用 UI 和 Windows PowerShell）。 若要完成本演练中的步骤，你必须设置一个实验室环境，并按照[为 Windows Server 2012 R2 中的 AD FS 设置实验室环境](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)中的步骤进行操作。

### <a name="advanced-scenarios"></a>高级方案
在 Windows Server 2012 R2 的 AD FS 中实施条件访问控制的其他示例包括：

-   仅当此用户的标识已使用 MFA 进行验证时，才允许访问受 AD FS 保护的应用程序

    可以使用以下代码：

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessWithMFA"
    c:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   仅当访问请求来自已注册到用户的已加入工作区的设备时，才允许访问受 AD FS 保护的应用程序

    可以使用以下代码：

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessFromRegisteredWorkplaceJoinedDevice"
    c:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   仅当访问请求来自已注册到已加入工作区的设备时，才允许访问受 AD FS 保护的应用程序，该设备已注册到其标识已使用 MFA 进行验证的用户

    可以使用以下代码

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAOnRegisteredWorkplaceJoinedDevice"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   仅当访问请求来自其标识已使用 MFA 进行验证的用户时，才允许对受 AD FS 保护的应用程序进行 extranet 访问。

    可以使用以下代码：

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAForExtranetAccess"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value =~ "^(?i)false$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

## <a name="see-also"></a>另请参阅
[操作实例指南：使用条件访问控制](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md) 
 管理风险[为 Windows Server 2012 R2 中的 AD FS 设置实验室环境](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
