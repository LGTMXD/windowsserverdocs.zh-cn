---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: 创建规则以将 LDAP 属性作为声明发送
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 938e82f5318bc374fd3f89bf5354c2fc447a9723
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967204"
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>创建规则以将 LDAP 属性作为声明发送


使用 "以声明方式发送 LDAP 属性" 规则模板 Active Directory 联合身份验证服务 \( AD FS \) ，你可以创建一个规则，该规则将从轻型目录访问协议 \( LDAP 属性存储中选择属性 \) ，如 Active Directory，以将其作为声明发送给信赖方。 例如，你可以使用此规则模板创建一个发送 LDAP 属性作为声明规则，该规则将从**displayName**和**telephoneNumber** Active Directory 属性中提取经过身份验证的用户的属性值，然后将这些值作为两个不同的传出声明发送。

你还可以使用此规则发送所有用户的组成员身份。 如果要仅发送单个组成员身份，请使用“以声明方式发送组成员身份”规则模板。 你可以使用以下过程通过 AD FS 管理 "管理单元来创建声明规则 \- 。

若要完成此过程，至少需要是本地计算机上的**管理员**组或等效组中的成员。  查看有关使用适当帐户和[本地和域默认组](https://go.microsoft.com/fwlink/?LinkId=83477)中组成员身份的详细信息。

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>创建规则以在 Windows Server 2016 中将 LDAP 属性作为信赖方信任的声明发送

1.  在服务器管理器中，单击“工具”，选择“AD FS 管理”********。

2.  在控制台树中的 " **AD FS**下，单击"**信赖方信任**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

3.  右键 \- 单击所选的信任，然后单击 "**编辑声明颁发策略**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)

4.  在 "**编辑声明颁发策略**" 对话框中的 "**颁发转换规则**" 下，单击 "**添加规则**" 以启动规则向导。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)

5.  在 "**选择规则模板**" 页上的 "**声明规则模板**" 下，选择 "**以声明方式从列表发送 LDAP 属性**"，然后单击 "**下一步**"。
![创建规则](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)

6.  在 "**声明规则名称**" 下的 "**配置规则**" 页面上，键入此规则的 "显示名称"，选择 "**属性存储**"，然后选择 LDAP 属性，并将其映射到 "传出声明类型"。
![创建规则](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)

7.  单击“完成”按钮。****

8.  在 "**编辑声明规则**" 对话框中，单击 **"确定"** 保存规则。

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>创建规则以在 Windows Server 2016 中将 LDAP 属性作为声明提供方信任的声明发送

1.  在服务器管理器中，单击“工具”，选择“AD FS 管理”********。

2.  在控制台树中的 " **AD FS**下，单击"**声明提供方信任**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)

3.  右键 \- 单击所选的信任，然后单击 "**编辑声明规则**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)

4.  在 "**编辑声明规则**" 对话框中的 "**接受转换规则**" 下，单击 "**添加规则**" 以启动规则向导。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)

5.  在 "**选择规则模板**" 页上的 "**声明规则模板**" 下，选择 "**以声明方式从列表发送 LDAP 属性**"，然后单击 "**下一步**"。
![创建规则](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)

6.  在 "**声明规则名称**" 下的 "**配置规则**" 页面上，键入此规则的 "显示名称"，选择 "**属性存储**"，然后选择 LDAP 属性，并将其映射到 "传出声明类型"。
![创建规则](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)

7.  单击“完成”按钮。****

8.  在 "**编辑声明规则**" 对话框中，单击 **"确定"** 保存规则。



## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>创建将 LDAP 属性作为 Windows Server 2012 R2 的声明进行发送的规则

1.  在服务器管理器中，单击“工具”，选择“AD FS 管理”********。

2.  在控制台树中的 " **AD FSAD FS \\ 信任关系**" 下，单击 "**声明提供方**信任或**信赖方信任**"，然后在要创建此规则的列表中单击特定信任。

3.  右键 \- 单击所选的信任，然后单击 "**编辑声明规则**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)

4.  在 "**编辑声明规则**" 对话框中，根据所编辑的信任和要在其中创建此规则的规则集，选择下列选项卡之一，然后单击 "**添加规则**" 以启动与该规则集关联的规则向导：

    -   **接受转换规则**

    -   **颁发转换规则**

    -   **颁发授权规则**

    -   **委派授权规则** 
 ![创建规则](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  在 "**选择规则模板**" 页上的 "**声明规则模板**" 下，选择 "**以声明方式从列表发送 LDAP 属性**"，然后单击 "**下一步**"。
![创建规则](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)

6.  在 "**声明规则名称**" 下的 "**配置规则**" 页上，键入此规则的显示名称，在 "**属性存储**" 下选择 " **ACTIVE DIRECTORY**"，然后在 "**将 ldap 属性映射到传出声明类型**" 下，从下拉列表中选择所需的**LDAP 属性**和相应的**传出声明类型**类型 \- 。

    对于要作为此规则的一部分发出声明的每个 Active Directory 属性，必须在不同的行上选择新的 LDAP 属性和传出声明类型对。
![创建规则](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)
7.  单击“完成”按钮。****

8.  在 "**编辑声明规则**" 对话框中，单击 **"确定"** 保存规则。

## <a name="additional-references"></a>其他参考
[配置声明规则](Configure-Claim-Rules.md)

[清单：为信赖方信任创建声明规则](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913578(v=ws.11))

[清单：为声明提供方信任创建声明规则](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913564(v=ws.11))

[何时使用授权声明规则](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)

[声明的角色](../../ad-fs/technical-reference/The-Role-of-Claims.md)

[声明规则的角色](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)
