---
ms.assetid: 9a06cd41-426f-4cb9-89cf-f5be730e0b79
title: Active Directory 域服务的新增功能
ms.topic: article
author: Femila
ms.author: billmath
ms.date: 05/31/2017
ms.openlocfilehash: 5f91e89e94a25eff1666de05d59415a1d84d9822
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938769"
---
# <a name="whats-new-in-active-directory-domain-services"></a>Active Directory 域服务的新增功能

>适用于：Windows Server 2016

Active Directory 域服务 () AD DS 中的以下新功能可提高组织保护 Active Directory 环境安全的能力，并帮助他们迁移到仅限云的部署和混合部署，其中某些应用程序和服务托管在云中，而其他应用程序和服务托管在本地。 这些改进包括：

-   [特权访问管理](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services)

- [通过 Azure Active Directory 联接将云功能扩展到 Windows 10 设备](/azure/active-directory/devices/overview)

- [将已加入域的设备连接到 Windows 10 体验 Azure AD](/azure/active-directory/devices/hybrid-azuread-join-plan)

- [在组织中启用 Microsoft Passport for Work](/windows/security/identity-protection/hello-for-business/hello-identity-verification)

-  [弃用文件复制服务 (FRS) 和 Windows Server 2003 功能级别](ad-ds/active-directory-functional-levels.md)


## <a name="privileged-access-management"></a><a name="BKMK_PAM"></a>特权访问管理
特权访问管理 (PAM) 可帮助减轻因凭据盗窃技术（例如传递哈希、鱼叉式的网络钓鱼和类似类型的攻击）引起的 Active Directory 环境的安全问题。 它提供了一个新的管理访问解决方案，该解决方案是通过使用 Microsoft Identity Manager (MIM) 配置的。 PAM 引入：

-   由 MIM 预配的新堡垒 Active Directory 林。 堡垒林与现有林有特殊的 PAM 信任。 它提供了一个新的 Active Directory 环境，该环境已知不会有任何恶意活动，并与现有林隔离以使用特权帐户。

-   MIM 中的新进程，用于请求管理权限，以及基于请求批准的新工作流。

-   新的卷影安全主体 (在堡垒林中由 MIM 在管理权限请求的响应中预配) 组。 影子安全主体有一个属性，该属性引用现有林中管理组的 SID。 这允许卷影组访问现有林中的资源，而无需更改任何 (Acl) 的访问控制列表。

-   过期链接功能，可在影子组中启用时间绑定成员身份。 用户可以添加到组中，只需足够的时间来执行管理任务。 时间绑定成员身份由传播到 Kerberos 票证生存期的生存时间 (TTL) 值来表示。

    > [!NOTE]
    > 过期链接适用于所有链接的属性。 但组和用户之间的成员/成员链接属性关系是唯一的示例，其中的一个完整解决方案（例如 PAM）已预先配置为使用过期链接功能。

-   KDC 增强功能内置于 Active Directory 域控制器中，以便在用户在管理组中具有多个时间绑定成员身份的情况下，将 Kerberos 票证生存期限制为尽可能低的生存时间 (TTL) 值。 例如，如果将添加到时间绑定组 A，则当你登录时，Kerberos 票证授予票证 (TGT) 生存期等于在组 A 中剩余的时间。如果你也是另一个受时间限制的组 B 的成员，而该组的 TTL 低于组 A，则 TGT 生存期等于您在组 B 中剩余的时间。

-   新的监视功能可帮助您轻松识别请求访问的人员、授予的访问权限以及执行的活动。

**要求**

-   Microsoft 标识管理器

-   Windows Server 2012 R2 或更高版本的 Active Directory 林功能级别。

## <a name="azure-ad-join"></a><a name="BKMK_AzureADJoin"></a>Azure AD 联接
Azure Active Directory 联接增强了企业、商业和 EDU 客户的标识体验-改进了企业和个人设备的功能。

优点：

-   公司拥有的 Windows 设备上**的新式设置的可用性**。 氧气服务不再需要个人 Microsoft 帐户：它们现在会关闭用户的现有工作帐户以确保合规性。 氧气 Services 将在加入本地 Windows 域的 Pc 上工作，以及 "加入" Azure AD 租户 ( "云域" ) 的 Pc 和设备。 这些设置包括：

    -   漫游或个性化，辅助功能设置和凭据

    -   备份和还原

    -   使用工作帐户访问 Microsoft Store

    -   动态磁贴和通知

-   访问移动设备上的**组织资源** (手机、无法加入 Windows 域的 phablets) ，无论它们是企业拥有还是 BYOD

-   **单一登录**到 Office 365 和其他组织应用、网站和资源。

-   在**BYOD 设备上**，将工作帐户 (从本地域或 Azure AD) 添加到个人拥有的设备，并通过应用和 WEB 使用 SSO 来处理资源，从而帮助确保符合新功能（如条件帐户控制和设备健康状况证明）。

-   通过**mdm 集成**，你可以自动将设备注册到 MDM (Intune 或第三方) 

-   为组织中的多个用户**设置 "展台" 模式和共享设备**

-   **开发人员体验**使你能够使用共享编程堆栈来构建满足企业和个人上下文需求的应用。

-   **映像**选项可让你在首次运行体验期间，选择映像并允许用户直接配置公司拥有的设备。

有关详细信息，请参阅适用于[企业的 Windows 10：使用设备进行工作的方式](/azure/active-directory/devices/overview)。

## <a name="microsoft-passport"></a><a name="BKMK_IDLocker"></a>Microsoft Passport
Microsoft Passport 是一种新的基于密钥的身份验证方法，组织和消费者超出了密码。 这种形式的身份验证依赖于安全漏洞、盗窃和诈骗网络的凭据。

用户使用已链接到证书或非对称密钥对的信息，在设备上登录到带有生物识别或 PIN 的日志。 标识提供者 (Idp) 通过将用户的公钥映射到 IDLocker 来验证用户，并通过一次性密码 (OTP) 、Phonefactor 或其他通知机制来提供登录信息。

有关详细信息，请参阅[使用不带密码的身份验证身份 Microsoft Passport](/windows/security/identity-protection/hello-for-business/hello-identity-verification)

## <a name="deprecation-of-file-replication-service-frs-and-windows-server-2003-functional-levels"></a><a name="BKMK_FRSDeprecation"></a>弃用文件复制服务 (FRS) 和 Windows Server 2003 功能级别
尽管文件复制服务 (FRS) 并且 Windows Server 2003 功能级别在以前版本的 Windows Server 中已弃用，但这会导致不再支持 Windows Server 2003 操作系统。 因此，应从域中删除任何运行 Windows Server 2003 的域控制器。 应将域和林功能级别至少提升到 Windows Server 2008，以防止将运行早期版本 Windows Server 的域控制器添加到环境中。

在 Windows Server 2008 及更高的域功能级别，分布式文件服务 (DFS) 复制用于在域控制器之间复制 SYSVOL 文件夹内容。 如果在 Windows Server 2008 或更高的域功能级别创建新的域，系统会自动使用 DFS 复制来复制 SYSVOL。 如果在较低的功能级别创建域，则在复制 SYSVOL 时，需从使用 FRS 复制迁移到使用 DFS 复制。 有关迁移步骤，可以参阅 [TechNet 上的过程](../storage/dfs-replication/migrate-sysvol-to-dfsr.md)，也可参阅[存储团队文件柜博客上的简化步骤集](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)。

仍支持 Windows Server 2003 域和林功能级别，但如果) 可能，组织应将功能级别提升到 Windows Server 2008 (或更高级别，以确保 SYSVOL 复制兼容性和将来支持。 此外，更高的功能级别还提供了许多其他的优势和功能。 有关详细信息，请参阅以下资源：

-   [理解 Active Directory(R) 域服务 (AD DS) 功能级别](ad-ds/active-directory-functional-levels.md)

-   [提升域功能级别](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753104(v=ws.11))

-   [提升林功能级别](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730985(v=ws.11))

