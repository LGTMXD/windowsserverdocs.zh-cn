---
ms.assetid: 826974ea-3635-40df-aa37-77dd12a363c8
title: 清单-配置帐户伙伴组织
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 409ad0704371237418eb38c0c81893b6e3d01e40
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854180"
---
# <a name="checklist-configuring-the-account-partner-organization"></a>清单︰ 配置帐户伙伴组织

帐户伙伴组织包含将访问 Web 的用户\-基于资源伙伴中的应用程序。 此组织中的管理员必须使用 AD FS 管理管理单元\-才能创建信赖方信任来表示它们资源伙伴组织之间的信任关系。 反过来，资源伙伴管理员必须创建每个帐户伙伴组织，他们想要信任的声明提供方信任。  
  
此清单包括用于在帐户伙伴组织中部署 Active Directory 联合身份验证服务 \(AD FS\) 的任务。 它还包括用于配置的组件所需建立一个多任务\-一半联合合作关系。  
  
如果正在部署 [Web SSO 设计](https://technet.microsoft.com/library/dd807033.aspx), ，无需按照此清单。 但是，您是否需要完成此清单，若要成功部署中的任务 [联合 Web SSO 设计](https://technet.microsoft.com/library/dd807050.aspx)。  
  
> [!IMPORTANT]  
> 请确保资源伙伴组织中的管理员，如下所示中的指导 [核对清单︰ 配置资源伙伴组织](Checklist--Configuring-the-Resource-Partner-Organization.md) 以确保所有必需的部署任务将会完成若要成功创建第二个半个联合合作关系。  
  
> [!NOTE]  
> 按顺序完成此清单中的任务。 当某个参考连接将你转至某个过程时，应在完成该过程中的步骤之后返回此主题，以便你可以继续执行此清单中的其他任务。  
  
![配置帐户伙伴组织](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**核对清单：配置帐户伙伴组织**  
  
||任务|参考|  
|-|--------|-------------|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|如果你当前在生产环境中使用现有的 AD FS 1.0 或1.1 部署，请参阅右侧的链接，了解有关如何将设置从当前联合身份验证服务迁移到新 AD FS 联合身份验证服务的信息。 如果你在组织中首次使用 AD FS 部署 AD FS，则可以跳过此步骤，并继续执行此清单中的下一项任务，以了解有关如何设置新的帐户伙伴组织的信息。|![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[计划迁移到 AD FS 2.0](https://technet.microsoft.com/library/ff678044.aspx)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|根据您的部署目标，查看有关用户提供对联合应用程序的访问权限所需的组件的信息。|![配置帐户伙伴组织，为](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[你的 Active Directory 用户提供对声明感知应用程序和服务的访问权限](https://technet.microsoft.com/library/dd807071.aspx)<p>![配置帐户伙伴组织向](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Active Directory 用户提供对其他组织的应用程序和服务的访问权限](https://technet.microsoft.com/library/dd807123.aspx)<p>![配置帐户伙伴组织向](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[另一组织中的用户提供对声明感知应用程序和服务的访问权限](https://technet.microsoft.com/library/dd807099.aspx)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|确定哪些 AD FS 设计此帐户伙伴组织将与相关联。|![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[WEB SSO 设计](https://technet.microsoft.com/library/dd807033.aspx)<p>![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[联合 WEB SSO 设计](https://technet.microsoft.com/library/dd807050.aspx)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|在开始部署 AD FS 服务器之前，请查看;1. 选择 "Windows 内部数据库" \(WID\) 或 SQL Server 以存储 AD FS 配置数据库 2\) 优点和缺点。AD FS 部署拓扑类型及其关联的服务器布局和网络布局建议\)。|![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[确定 AD FS 部署拓扑](https://technet.microsoft.com/library/gg982491.aspx)<p>![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 部署拓扑注意事项](https://technet.microsoft.com/library/gg982489.aspx)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|查看 AD FS 容量规划指南以确定联合身份验证服务器和联合服务器代理服务器应在生产环境中使用的正确号码。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[为 AD FS 服务器容量](https://technet.microsoft.com/library/gg749899.aspx)配置帐户伙伴组织规划|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|为了有效地规划和实施帐户合作伙伴部署的物理拓扑，确定你的 AD FS 设计需要一个或多个联合服务器或联合服务器代理。|![配置帐户伙伴组织](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[核对清单：设置联合服务器](Checklist--Setting-Up-a-Federation-Server.md)<p>![配置帐户伙伴组织](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[核对清单：设置联合服务器代理](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|确定想要添加到 AD FS 的属性存储的类型。 然后，将属性存储区中使用 AD FS 管理管理单元添加\-中。|![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[属性存储的角色](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<p>![配置帐户伙伴组织](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[添加属性存储](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|如果需要向使用 AD FS 1.0 或1.1 联合身份验证服务的资源伙伴发送声明或使用声明，请参阅右侧的链接，了解有关如何配置 AD FS 以与以前版本的 AD FS 进行互操作的信息。 如果资源伙伴组织也使用 AD FS 以发送或使用您的组织声明，您可以跳过此步骤，然后继续进行此检查表的下一任务。|![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[规划以实现与 AD FS 1.x 的互操作性](https://technet.microsoft.com/library/ff678040.aspx)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|部署帐户伙伴组织中的第一个联合服务器后，创建使用 AD FS 管理管理单元的信赖方信任关系\-中。 可以通过手动输入有关资源伙伴的数据，或者使用资源伙伴组织管理员提供给你的联合元数据 URL，来创建信赖方信任。 可以使用联合元数据来自动检索资源伙伴的数据。 **注意︰** 如果资源伙伴发布其联合元数据，或者可以提供它为您要使用的文件副本，我们建议可以节省时间，因为自动检索数据。|![配置帐户伙伴组织](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[手动创建信赖方信任](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)<p>![配置帐户伙伴组织](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[使用联合元数据创建信赖方信任](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|根据您的组织的需要，创建一个或多个声明规则设置为指定每个信赖方信任 AD FS 管理管理单元中\-中，以便将相应地颁发的声明。|![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[核对清单：创建信赖方信任的声明规则](Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|如果尚不存在，则必须创建索赔说明，将满足您的组织的需求。 AD FS 附带了一组默认的公开的声明说明在 AD FS 管理管理单元中\-中。|![配置帐户伙伴组织](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[添加声明说明](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|确定您的组织将需要使用标识委托来授权或约束指定的帐户"作为"或模拟其他用户。 这通常是一项要求时前\-结束的 Web 应用程序必须与后交互\-结束的 Web 服务。|![配置帐户伙伴组织](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[何时使用身份委派](https://technet.microsoft.com/library/dd807122.aspx)|  
|![配置帐户伙伴组织](media/icon_checkboxo.gif)|准备联合身份验证的客户端计算机︰<p>-到客户端浏览器的受信任的站点列表中添加帐户伙伴联合身份验证服务器的 URL。<br />-使用组策略将相应的安全套接字层 \(SSL\) 证书推送到客户端计算机。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[在帐户伙伴中配置帐户伙伴组织准备客户端计算机](https://technet.microsoft.com/library/dd807114(v=ws.11).aspx)<p>![配置帐户伙伴组织](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[配置客户端计算机以信任帐户联合服务器](Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)<p>![配置帐户伙伴组织](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[使用组策略将证书分发到客户端计算机](Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)| 
