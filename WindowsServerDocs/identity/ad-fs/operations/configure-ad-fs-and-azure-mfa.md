---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: 配置 AD FS 2016 和 Azure MFA
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0a3a08df3789e607a5f154a4735c153867e6046d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86960569"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>将 Azure MFA 配置为具有 AD FS 的身份验证提供程序

如果你的组织与 Azure AD 联合，你可以使用 Azure 多重身份验证保护 AD FS 资源（包括本地和云中的资源）。 Azure MFA 使你可以消除密码，并提供更安全的身份验证方法。  从 Windows Server 2016 开始，你现在可以将 Azure MFA 配置为进行主要身份验证，或将其用作附加身份验证提供程序。 
  
与 Windows Server 2012 R2 中的 AD FS 不同，AD FS 2016 Azure MFA 适配器与 Azure AD 直接集成，无需本地 Azure MFA 服务器。   Azure MFA 适配器内置于 Windows Server 2016，无需其他安装。


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>向 AD FS 注册 Azure MFA 的用户

AD FS 不支持内联 &#34;&#34; 或注册 Azure MFA 安全验证信息，例如电话号码或移动应用。 这意味着，用户必须先访问防，然后 [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx) 才能使用 AZURE MFA 对 AD FS 应用程序进行身份验证。 当尚未 Azure AD 防的用户尝试在 AD FS 上使用 Azure MFA 进行身份验证时，他们将收到 AD FS 错误。  作为 AD FS 管理员，你可以自定义此错误体验以引导用户转到 proofup 页。  您可以使用 onload.js 自定义来检测 AD FS 页面内的错误消息字符串，并显示一条新消息来引导用户访问 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) ，然后重新尝试身份验证，从而执行此操作。 有关详细指南，请参阅本文中的 "自定义 AD FS 网页，指导用户注册 MFA 验证方法"。

>[!NOTE]
> 之前，用户需要通过 MFA 进行身份验证，以便进行注册（ [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx) 例如通过快捷方式进行访问 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) ）。  现在，尚未注册 MFA 验证信息的 AD FS 用户只能通过 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) 使用主要身份验证（例如 Windows 集成身份验证或用户名和 AD FS 密码）通过快捷方式访问 Azure AD&#34;的 proofup 页面。  如果用户未配置任何验证方法，Azure AD 将执行内联注册，用户可在其中看到消息 &#34;你的管理员要求你将此帐户设置为进行额外安全验证&#34;，然后用户可以 &#34;选择立即&#34; 设置。
> 在访问 proofup 页时，系统仍会提示已配置至少一个 MFA 验证方法的用户提供 MFA。

## <a name="recommended-deployment-topologies"></a>建议的部署拓扑

### <a name="azure-mfa-as-primary-authentication"></a>作为主要身份验证的 Azure MFA

使用 Azure MFA 作为 AD FS 的主要身份验证有几个重要原因：

 - 若要避免登录到 Azure AD、Office 365 和其他 AD FS 应用的密码
 - 若要通过要求额外的因素（例如密码之前的验证码）来保护基于密码的登录

如果要使用 Azure MFA 作为 AD FS 中的主要身份验证方法来实现这些优势，你可能还希望通过在 AD FS 中提示其他因素来保证使用 Azure AD 条件性访问，包括 &#34;true MFA&#34;。

你现在可以通过将 Azure AD 域设置配置为在本地进行 MFA （将 &#34;SupportsMfa&#34; 设置为 $True）来执行此操作。  在此配置中，Azure AD AD FS 会提示执行额外的身份验证，或 &#34;true MFA&#34; 用于需要它的条件性访问方案。  

如上所述，尚未注册的任何 AD FS 用户（配置 MFA 验证信息）都应通过自定义的 AD FS 错误页进行访问，以便访问 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) 配置验证信息，然后重试 AD FS 登录。  
由于 Azure MFA 作为主要副本视为单个因素，因此在初始配置后，用户需要提供额外的因素来管理或更新 Azure AD 中的验证信息，或访问需要 MFA 的其他资源。

>[!NOTE]
> 使用 ADFS 2019，需要修改 Active Directory 声明提供方信任的定位点声明类型，并将其从 windowsaccountname 修改为 UPN。 执行下面提供的 PowerShell cmdlet。 这不会影响 AD FS 场的内部运行。 你可能会注意到，在做出此项更改后，可能会再次提示用户输入凭据。 再次登录后，最终用户将看不到任何差别。 

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Azure MFA 作为 Office 365 的附加身份验证

以前，如果你希望将 Azure MFA 作为 Office 365 或其他信赖方 AD FS 的附加身份验证方法，则最好的做法是将 Azure AD 配置为执行复合 MFA，其中主要身份验证在 AD FS 本地执行，而 MFA 由 Azure AD 触发。 现在，可以使用 Azure MFA 作为 AD FS 中的其他身份验证，前提是将 domain SupportsMfa 设置设置为 $True。  

如上所述，尚未注册的任何 AD FS 用户（配置 MFA 验证信息）都应通过自定义的 AD FS 错误页进行访问，以便访问 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) 配置验证信息，然后重试 AD FS 登录。  

## <a name="pre-requisites"></a>先决条件

使用 Azure MFA 对 AD FS 进行身份验证时，需要以下先决条件：  
  
- [具有 Azure Active Directory 的 Azure 订阅](https://azure.microsoft.com/pricing/free-trial/)。  
- [Azure 多重身份验证](/azure/active-directory/authentication/concept-mfa-howitworks) 


> [!NOTE]
> Azure AD 和 Azure MFA 包含在 Azure AD Premium 和企业移动性套件（EMS）中。  如果有这样的一种，则不需要单独订阅。

- Windows Server 2016 AD FS 本地环境。  
   - 服务器需要能够通过端口443与以下 Url 通信。
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- 你的本地环境[与 Azure AD 联合。](/azure/active-directory/hybrid/how-to-connect-install-custom#configuring-federation-with-ad-fs)  
- Windows [PowerShell 的 windows Azure Active Directory 模块](/powershell/module/azuread/?view=azureadps-2.0)。  
- 使用 Azure AD PowerShell 配置 Azure AD 实例的全局管理员权限。  
- 用于配置 Azure MFA 的 AD FS 场的企业管理员凭据。

## <a name="configure-the-ad-fs-servers"></a>配置 AD FS 服务器

若要完成 Azure MFA for AD FS 的配置，需要按照所述步骤配置每个 AD FS 服务器。 

>[!NOTE]
>确保在场中的**所有**AD FS 服务器上执行这些步骤。 如果场中有多个 AD FS 服务器，则可以使用 Azure AD PowerShell 远程执行所需的配置。  

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>步骤1：使用 cmdlet 为每台 AD FS 服务器上的 Azure MFA 生成证书 `New-AdfsAzureMfaTenantCertificate`

你需要做的第一件事就是生成一个用于 Azure MFA 的证书。  可以使用 PowerShell 完成此操作。  可以在 "本地计算机" 证书存储中找到生成的证书，并将其标记为 "使用者名称"，其中包含用于 Azure AD 目录的 TenantID。

![AD FS 和 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  

请注意，TenantID 是 Azure AD 中的目录的名称。  使用以下 PowerShell cmdlet 生成新证书。  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  

![AD FS 和 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>步骤2：向 Azure 多重身份验证客户端服务主体添加新凭据

为了使 AD FS 服务器能够与 Azure 多重身份验证客户端进行通信，需要将凭据添加到 Azure 多重身份验证客户端的服务主体。 使用 cmdlet 生成的证书 `New-AdfsAzureMFaTenantCertificate` 将充当这些凭据。 使用 PowerShell 执行以下操作，将新凭据添加到 Azure 多重身份验证客户端服务主体。  

> [!NOTE]
> 若要完成此步骤，需要使用 PowerShell 连接到 Azure AD 的实例 `Connect-MsolService` 。  这些步骤假定你已通过 PowerShell 进行连接。  有关信息，请参阅[ `Connect-MsolService` 。](/previous-versions/azure/dn194123(v=azure.100))  

**将证书设置为 Azure 多因素身份验证客户端的新凭据**  

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> 需要在服务器场中的所有 AD FS 服务器上运行此命令。  对于 Azure 多重身份验证客户端，未将证书设置为新凭据的服务器上的 Azure AD MFA 将会失败。

> [!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720 是 Azure 多重身份验证客户端的 GUID。  
  
## <a name="configure-the-ad-fs-farm"></a>配置 AD FS 场  
  
完成每个 AD FS 服务器上的上一节后，使用[AdfsAzureMfaTenant](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) Cmdlet 设置 Azure 租户信息。 对于 AD FS 场，此 cmdlet 只需要执行一次。

打开 PowerShell 提示符，并使用[AdfsAzureMfaTenant](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) cmdlet 输入你自己的*tenantId* 。 对于使用 Microsoft Azure 政府云的客户，请添加 `-Environment USGov` 参数：

> [!NOTE]
> 需要在服务器场中的每个服务器上重新启动 AD FS 服务，这些更改才会生效。 为了最大限度地减少影响，每个 AD FS 服务器一次一个地从 NLB 旋转，并等待所有连接排出。

```powershell
Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720
```

![AD FS 和 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)

没有最新 Service Pack 的 Windows Server 不支持 `-Environment` [AdfsAzureMfaTenant](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata) cmdlet 的参数。 如果使用 Azure 政府云，并且之前的步骤未能配置 Azure 租户，原因是缺少 `-Environment` 参数，请完成以下步骤手动创建注册表项。 如果上一个 cmdlet 正确注册了你的租户信息，或者你不在 Azure 政府版云中，请跳过这些步骤：

1. 在 AD FS 服务器上打开**注册表编辑器**。
1. 导航到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ADFS`。 创建以下注册表项值：

    | 注册表项       | 值 |
    |--------------------|-----------------------------------|
    | SasUrl             | https://adnotifications.windowsazure.us/StrongAuthenticationService.svc/Connector |
    | StsUrl             | https://login.microsoftonline.us |
    | ResourceUri        | https://adnotifications.windowsazure.us/StrongAuthenticationService.svc/Connector |

1. 在服务器场中的每个服务器上重新启动 AD FS 服务，这些更改才会生效。 为了最大限度地减少影响，每个 AD FS 服务器一次一个地从 NLB 旋转，并等待所有连接排出。

此后，你将看到 Azure MFA 作为 intranet 和 extranet 使用的主要身份验证方法提供。

![AD FS 和 MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>续订和管理 AD FS Azure MFA 证书

以下指南将引导你了解如何管理 AD FS 服务器上的 Azure MFA 证书。
默认情况下，使用 Azure MFA 配置 AD FS 时，通过 PowerShell cmdlet 生成的证书 `New-AdfsAzureMfaTenantCertificate` 有效期为2年。  若要确定证书过期的接近程度，然后续订和安装新证书，请使用以下过程。

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>评估 AD FS Azure MFA 证书到期日期

在每个 AD FS 服务器上，在本地计算机的 "我的应用商店" 中，有一个自签名证书，&#34;OU = Microsoft AD FS Azure MFA&#34; 在颁发者和主题中。  这是 Azure MFA 证书。  检查每个 AD FS 服务器上此证书的有效期，以确定到期日期。  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>新建 AD FS 每个 AD FS 服务器上的 Azure MFA 证书

如果证书的有效期即将结束，请在每个 AD FS 服务器上生成新的 Azure MFA 证书，开始续订过程。 在 PowerShell 命令窗口中，使用以下 cmdlet 在每个 AD FS 服务器上生成新证书：

> [!CAUTION]
> 如果证书已过期，请不要将参数添加 `-Renew $true` 到下面的命令中。 在这种情况下，现有过期证书将替换为新证书，而不是保留原样，并创建其他证书。

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

如果证书尚未过期，则会生成一个新证书，该证书从未来2天到2天 + 2 年都有效。 AD FS 和 Azure MFA 操作不受此 cmdlet 或新证书影响。 （请注意：此2天延迟是特意的，并提供执行以下步骤以在租户中配置新证书的时间，然后 AD FS 开始将它用于 Azure MFA。）

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>在 Azure AD 租户中配置每个新 AD FS Azure MFA 证书

使用 Azure AD PowerShell 模块，针对每个 AD FS 服务器上的每个新证书，按如下所示更新 Azure AD 租户设置（注意：必须先使用连接到租户， `Connect-MsolService` 才能运行以下命令）。

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $newcert
```

如果以前的证书已过期，请重新启动 AD FS 服务选取新证书。 如果证书过期之前已续订证书，则无需重新启动 AD FS 服务。

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>验证新证书将用于 Azure MFA

新证书生效后，AD FS 将在几个小时内将其挑选并开始使用各自的 Azure MFA 证书到一天。  出现这种情况后，在每个服务器上都将看到一个事件，该事件记录在 AD FS Admin 事件日志中，其中包含以下信息：

```
Log Name:      AD FS/Admin
Source:        AD FS
Date:          2/27/2018 7:33:31 PM
Event ID:      547
Task Category: None
Level:         Information
Keywords:      AD FS
User:          DOMAIN\adfssvc
Computer:      ADFS.domain.contoso.com
Description:
The tenant certificate for Azure MFA has been renewed.  

TenantId: contoso.onmicrosoft.com.
Old thumbprint: 7CC103D60967318A11D8C51C289EF85214D9FC63.
Old expiration date: 9/15/2019 9:43:17 PM.
New thumbprint: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF.
New expiration date: 2/27/2020 2:16:07 AM.
```

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>自定义 AD FS 网页，指导用户注册 MFA 验证方法

使用以下示例为尚未防（已配置 MFA 验证信息）的用户自定义 AD FS 网页。

### <a name="find-the-error"></a>查找错误

首先，有几个不同的错误消息 AD FS 将在用户缺少验证信息时返回。
如果使用 Azure MFA 作为主要身份验证，则防用户将看到一个 AD FS 错误页面，其中包含以下消息：
```
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information.
        </div>
```
当尝试 Azure AD 作为附加身份验证时，防用户将看到一个包含以下消息的 AD FS 错误页：
```
<div id='mfaGreetingDescription' class='groupMargin'>For security reasons, we require additional information to verify your account (mahesh@jenfield.net)</div>
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            The selected authentication method is not available for &#39;username@contoso.com&#39;. Choose another authentication method or contact your system administrator for details.
        </div>
```

### <a name="catch-the-error-and-update-the-page-text"></a>捕获错误并更新页面文本

若要捕获错误并显示用户自定义指南，只需将 javascript 追加到作为 AD FS web 主题一部分的 onload.js 文件的末尾。  这允许你执行以下操作：
 - 搜索标识错误字符串
 - 提供自定义 web 内容。  

> [!NOTE]
> 有关如何自定义 onload.js 文件的一般指南，请参阅文章[AD FS 登录页的高级自定义](advanced-customization-of-ad-fs-sign-in-pages.md)。

下面是一个简单的示例，你可能想要扩展：

1. 在主 AD FS 服务器上打开 Windows PowerShell，并通过运行以下命令创建新的 AD FS Web 主题：
    
    ``` PowerShell
        New-AdfsWebTheme –Name ProofUp –SourceName default
    ``` 
2. 接下来，创建文件夹并导出默认 AD FS Web 主题：

    ``` PowerShell
       New-Item -Path 'c:\Theme' -ItemType Directory;Export-AdfsWebTheme –Name default –DirectoryPath c:\Theme
    ```
3. 在文本编辑器中打开 C:\Theme\script\onload.js 文件
4. 在 onload.js 文件的末尾追加以下代码
    
    ``` JavaScript
    //Custom Code
    //Customize MFA exception
    //Begin

    var domain_hint = "<YOUR_DOMAIN_NAME_HERE>";
    var mfaSecondFactorErr = "The selected authentication method is not available for";
    var mfaProofupMessage = "You will be automatically redirected in 5 seconds to set up your account for additional security verification. Once you have completed the setup, please return to the application you are attempting to access.<br><br>If you are not redirected automatically, please click <a href='{0}'>here</a>."
    var authArea = document.getElementById("authArea");
    if (authArea) {
        var errorMessage = document.getElementById("errorMessage");
        if (errorMessage) {
            if (errorMessage.innerHTML.indexOf(mfaSecondFactorErr) >= 0) {

                //Hide the error message
                var openingMessage = document.getElementById("openingMessage");
                if (openingMessage) {
                    openingMessage.style.display = 'none'
                }
                var errorDetailsLink = document.getElementById("errorDetailsLink");
                if (errorDetailsLink) {
                    errorDetailsLink.style.display = 'none'
                }

                //Provide a message and redirect to Azure AD MFA Registration Url
                var mfaRegisterUrl = "https://account.activedirectory.windowsazure.com/proofup.aspx?proofup=1&whr=" + domain_hint;
                errorMessage.innerHTML = "<br>" + mfaProofupMessage.replace("{0}", mfaRegisterUrl);
                window.setTimeout(function () { window.location.href = mfaRegisterUrl; }, 5000);
            }
        }
    }

    //End Customize MFA Exception
    //End Custom Code
    ```
    > [!IMPORTANT]
    > 需要更改 "<YOUR_DOMAIN_NAME_HERE>";使用你的域名。 例如：`var domain_hint = "contoso.com";`
    
5. 保存 onload.js 文件
6. 键入以下 Windows PowerShell 命令，将 onload.js 文件导入自定义主题：
    
    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}
    ```
7. 最后，通过键入以下 Windows PowerShell 命令，应用自定义 AD FS Web 主题：
    
    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName "ProofUp"
    ```

## <a name="next-steps"></a>后续步骤

[管理 AD FS 和 Azure MFA 使用的 TLS/SSL 协议和密码套件](manage-ssl-protocols-in-ad-fs.md)
