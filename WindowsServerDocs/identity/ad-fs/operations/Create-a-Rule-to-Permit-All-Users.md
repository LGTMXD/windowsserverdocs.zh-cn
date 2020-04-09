---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: 创建规则以允许所有用户
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 894857813115002f3998a9ab5000d57b944fd448
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816780"
---
# <a name="create-a-rule-to-permit-all-users"></a>创建规则以允许所有用户

在 Windows Server 2016 中，你可以使用**访问控制策略**来创建一个规则，该规则将允许所有用户访问信赖方。  在 Windows Server 2012 R2 中，使用 Active Directory 联合身份验证服务 \(AD FS\)中的 "**允许所有用户**" 规则模板，你可以创建一个授权规则，该规则将允许所有用户访问信赖方。 

你可以使用其他授权规则进一步限制访问。 有权从联合身份验证服务访问信赖方的用户可能仍会被信赖方拒绝服务。  
  
你可以使用下列过程，通过中的 AD FS 管理 "管理单元\-来创建声明规则。  
  
若要完成此过程，至少需要是本地计算机上的**管理员**组或等效组中的成员。  可在[本地默认组和域默认组](https://go.microsoft.com/fwlink/?LinkId=83477)中查看有关使用适合的帐户和组成员身份的详细信息。 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>创建规则以允许 Windows Server 2016 中的所有用户

1.  在服务器管理器中，单击 "**工具**"，然后选择 " **AD FS 管理**"。  
  
2.  在控制台树中的 " **AD FS**下，单击"**信赖方信任**"。 
![创建规则](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  右键单击要允许访问的**信赖方信任**，然后选择 "**编辑访问控制策略**"。  
![创建规则](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. 在访问控制策略中，选择 "**允许所有人**"，然后单击 "**应用** **" 和 "确定"** 。
![创建规则](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>创建规则以允许 Windows Server 2012 R2 中的所有用户 
  
1.  在服务器管理器中，单击 "**工具**"，然后选择 " **AD FS 管理**"。  
  
2.  在控制台树中的 " **AD FS\\信任关系"\\信赖方信任**"下，单击列表中你想要创建此规则的特定信任。  

3.  右键\-单击选定的信任，然后单击 "**编辑声明规则**"。  
![创建规则](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  在 "**编辑声明规则**" 对话框中，单击 "**颁发授权规则**" 选项卡或 "**委派授权规则**" 选项卡 \(根据所需的授权规则类型\)，然后单击 "**添加规则**" 以启动 "**添加授权声明规则向导**"。  
![创建规则](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  在 "**选择规则模板**" 页上的 "**声明规则模板**" 下，选择 "允许列表中的**所有用户**"，然后单击 "**下一步**"。  
![创建规则](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  在 "**配置规则**" 页上，单击 "**完成**"。  
  
7.  在 "**编辑声明规则**" 对话框中，单击 **"确定"** 保存规则。  

## <a name="additional-references"></a>其他参考 
[配置声明规则](Configure-Claim-Rules.md)  
 
[清单：为信赖方信任创建声明规则](https://technet.microsoft.com/library/ee913578.aspx)  
  
[何时使用授权声明规则](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[声明的角色](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[声明规则的角色](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
