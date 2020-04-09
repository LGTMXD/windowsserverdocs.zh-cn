---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: 清单-设置联合服务器代理
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: a9784a7c599f6b1f13d9773a376e40b678106123
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854590"
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>清单：设置联合服务器代理

此清单包含为 Active Directory 联合身份验证服务 \(AD FS\)中的联合服务器代理角色准备运行 Windows Server&reg; 2012 的服务器的部署任务。  
  
> [!NOTE]  
> 按顺序完成此清单中的任务。 当某个参考连接将你转至某个过程时，应在完成该过程中的步骤之后返回此主题，以便你可以继续执行此清单中的其他任务。  
  
![设置联合代理服务器](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**清单：设置联合服务器代理**  
  
||任务|参考|  
|-|--------|-------------|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|开始部署 AD FS 联合服务器代理之前，请查看 AD FS 部署拓扑类型及其相关服务器布局和网络布局建议。|设置联合代理服务器 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[确定 AD FS 部署拓扑](https://technet.microsoft.com/library/gg982491.aspx)<p>![设置联合代理服务器](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[规划联合服务器代理的位置](https://technet.microsoft.com/library/dd807130.aspx)<p>![设置联合代理服务器](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[以放置联合服务器代理](https://technet.microsoft.com/library/dd807048.aspx)|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|查看 AD FS 容量规划指南，以确定应该在生产环境中使用的适当数量的联合服务器代理。|![设置联合代理服务器](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[规划联合服务器代理容量](https://technet.microsoft.com/library/gg749898.aspx)|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|确定单个联合服务器代理或联合服务器代理场是否更适合你的部署。 **注意：** 联合服务器还执行联合服务器代理责任。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[在创建联合服务器代理时](https://technet.microsoft.com/library/dd807032.aspx)设置联合代理服务器<p>![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[在创建联合服务器代理场时](https://technet.microsoft.com/library/dd807082.aspx)设置联合代理服务器|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|确定是否将在帐户伙伴组织或资源伙伴组织的外围网络中创建此新的联合服务器代理。|![设置联合代理服务器](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[在帐户伙伴中查看联合服务器代理的角色](https://technet.microsoft.com/library/dd807109.aspx)<p>![设置联合代理服务器](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[检查资源伙伴中联合服务器代理的角色](https://technet.microsoft.com/library/dd807052.aspx)|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|在将成为联合服务器代理的计算机上安装 AD FS 之前，请阅读获取服务器身份验证证书的重要性-对于联合服务器代理场-在服务器场中的所有服务器之间添加或共享证书。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[为联合服务器代理](https://technet.microsoft.com/library/dd807054.aspx)设置联合代理服务器证书要求|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|有关如何在外围网络中更新域名系统 \(DNS\)，以便可以进行联合服务器和联合服务器代理的成功名称解析的详细信息，请查看 AD FS 设计指南中的信息。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[为联合服务器代理](https://technet.microsoft.com/library/dd807055.aspx)设置联合代理服务器名称解析要求 ![|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|确定联合服务器代理是否必须加入域。 尽管不需要将联合服务器代理加入到域中，但在将它们加入域时，使用远程管理和组策略功能可以更轻松地管理它们。|![设置联合代理服务器将](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[计算机加入域](Join-a-Computer-to-a-Domain.md)|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|根据外围网络中的 DNS 基础结构的配置方式，在组织中部署联合服务器代理之前，请先完成右侧主题中的一个过程。 **注意：** 请勿执行这两个过程。 读取[联合服务器代理的名称解析要求](https://technet.microsoft.com/library/dd807055.aspx)，以确定最适合组织需求的过程。|![设置联合代理服务器](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[在仅为外围网络提供服务的 DNS 区域中为联合服务器代理配置名称解析](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<p>设置联合代理服务器 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[在同时为外围网络和 Internet 客户端提供服务的 DNS 区域中为联合服务器代理配置名称解析](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|获取服务器身份验证证书后，必须将其安装在联合服务器代理的默认网站 Internet Information Services \(IIS\) 中。|![设置联合代理服务器会将](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[服务器身份验证证书导入到默认](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)网站|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|\(可选\) 作为从证书颁发机构 \(CA\)获取服务器身份验证证书的替代方法，可以使用 IIS 为联合服务器代理获取示例证书。<p>由于 IIS 会生成一个不是来自受信任源的\-自签名证书，因此仅在以下情况下才使用它创建自\-签名证书：<p>-必须在服务器与有限的已知用户组之间创建安全套接字层 \(SSL\) 通道<br />-当你必须排查第三\-方证书问题时，请**注意：** 使用自\-签名的服务器身份验证证书在生产环境中部署联合服务器代理不是最佳安全方案。|![设置联合代理服务器](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS：创建自\-签名服务器证书](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|在将成为联合服务器代理的计算机上安装联合身份验证服务代理角色服务。|![设置联合代理服务器](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[安装联合身份验证服务代理角色服务](Install-the-Federation-Service-Proxy-Role-Service.md)|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|使用 AD FSFederation Server Proxy 配置向导将计算机上的 AD FS 软件配置为充当联合服务器代理角色。|![设置联合代理服务器，请](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[为联合服务器代理角色配置计算机](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)|  
|![设置联合代理服务器](media/icon_checkboxo.gif)|使用事件查看器，验证已启动联合服务器代理服务。|设置联合代理服务器 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[验证联合服务器代理是否正常工作](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|  
