---
ms.assetid: ef83960f-d2cf-441f-b2b6-d97822ec7149
title: 创建规则以转换传入声明
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 754db25ee9480054c12959740909841ee46311ff
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956564"
---
# <a name="create-a-rule-to-transform-an-incoming-claim"></a>创建规则以转换传入声明


通过使用 Active Directory 联合身份验证服务 AD FS 中的 "**转换传入声明**" 规则模板 \( \) ，可以选择传入声明、更改其声明类型以及更改其声明值。 例如，你可以使用此规则模板创建一个规则，该规则使用传入组声明的相同声明值来发送角色声明。 当具有 "管理员" 值的传入组声明时，还可以使用此规则发送声明值为 "购买者" 的组声明，也可以只发送以结尾的用户主体名称 \( UPN \) 声明 @fabrikam 。

你可以使用以下过程通过 AD FS 管理 "管理单元来创建声明规则 \- 。

在本地计算机上， **Administrators**中的成员身份或同等身份是完成此过程的最低要求。  查看有关使用适当帐户和[本地和域默认组](https://go.microsoft.com/fwlink/?LinkId=83477)中组成员身份的详细信息。

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>在 Windows Server 2016 中创建规则以转换信赖方信任上的传入声明

1.  在服务器管理器中，单击“工具”，选择“AD FS 管理”********。

2.  在控制台树中的 " **AD FS**下，单击"**信赖方信任**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

3.  右键 \- 单击所选的信任，然后单击 "**编辑声明颁发策略**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)

4.  在 "**编辑声明颁发策略**" 对话框中的 "**颁发转换规则**" 下，单击 "**添加规则**" 以启动规则向导。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)

5.  在 "**选择规则模板**" 页上的 "**声明规则模板**" 下，从列表中选择 "**转换传入声明**"，然后单击 "**下一步**"。
![创建规则](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)

6.  在 "**配置规则**" 页上的 "**声明规则名称**" 下，键入此规则的显示名称。 在 "**传入声明类型**" 中，选择列表中的声明类型。 在 "**传出声明类型**" 中，选择列表中的声明类型，然后选择以下选项之一，这取决于组织的需求：

    -   **传递所有声明值**

    -   **将传入声明值替换为不同的传出声明值**

    -   **将传入电子 \- 邮件后缀声明替换为新的电子 \- 邮件后缀** 
 ![ 创建规则](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)

7.  单击“完成”按钮。****

8.  在 "**编辑声明规则**" 对话框中，单击 **"确定"** 保存规则。

> [!NOTE]
> 如果要设置使用 AD FS 颁发的声明的动态访问控制方案 \- ，请先在声明提供方信任上创建转换规则，然后在 "**传入声明类型**" 中键入传入声明的名称，或者，如果以前创建了声明说明，请从列表中选择它。 其次，在 "**传出声明类型**" 中选择所需的声明 URL，然后在信赖方信任上创建转换规则以发出设备声明。
>
> 有关动态访问控制方案的详细信息，请参阅[动态访问控制内容路线图](../../solution-guides/dynamic-access-control--scenario-overview.md)或[使用 AD FS AD DS 声明](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831504(v=ws.11))。

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>创建规则以在 Windows Server 2016 中的声明提供方信任上转换传入声明

1.  在服务器管理器中，单击“工具”，选择“AD FS 管理”********。

2.  在控制台树中的 " **AD FS**下，单击"**声明提供方信任**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)

3.  右键 \- 单击所选的信任，然后单击 "**编辑声明规则**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)

4.  在 "**编辑声明规则**" 对话框中的 "**接受转换规则**" 下，单击 "**添加规则**" 以启动规则向导。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)

5.  在 "**选择规则模板**" 页上的 "**声明规则模板**" 下，从列表中选择 "**转换传入声明**"，然后单击 "**下一步**"。
![创建规则](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)

6.  在 "**配置规则**" 页上的 "**声明规则名称**" 下，键入此规则的显示名称。 在 "**传入声明类型**" 中，选择列表中的声明类型。 在 "**传出声明类型**" 中，选择列表中的声明类型，然后选择以下选项之一，这取决于组织的需求：

    -   **传递所有声明值**

    -   **将传入声明值替换为不同的传出声明值**

    -   **将传入电子 \- 邮件后缀声明替换为新的电子 \- 邮件后缀** 
 ![ 创建规则](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)

7.  单击“完成”按钮。****

8.  在 "**编辑声明规则**" 对话框中，单击 **"确定"** 保存规则。

> [!NOTE]
> 如果要设置使用 AD FS 颁发的声明的动态访问控制方案 \- ，请先在声明提供方信任上创建转换规则，然后在 "**传入声明类型**" 中键入传入声明的名称，或者，如果以前创建了声明说明，请从列表中选择它。 其次，在 "**传出声明类型**" 中选择所需的声明 URL，然后在信赖方信任上创建转换规则以发出设备声明。
>
> 有关动态访问控制方案的详细信息，请参阅[动态访问控制内容路线图](../../solution-guides/dynamic-access-control--scenario-overview.md)或[使用 AD FS AD DS 声明](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831504(v=ws.11))。

## <a name="to-create-a-rule-to-transform-an-incoming-claim-in-windows-server-2012-r2"></a>创建规则以在 Windows Server 2012 R2 中转换传入声明

1.  在服务器管理器中，单击 "**工具**"，然后单击 " **AD FS 管理**"。

2.  在控制台树中的 " **AD FS \\ 信任关系**" 下，单击 "**声明提供方信任**或**信赖方信任**"，然后在要创建此规则的列表中单击特定信任。

3.  右键 \- 单击所选的信任，然后单击 "**编辑声明规则**"。
![创建规则](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)

4.  在 "**编辑声明规则**" 对话框中，选择下列选项卡，其中一个选项卡依赖于你正在编辑的信任和你要在哪个规则集中创建此规则，然后单击 "**添加规则**" 以启动与该规则集关联的规则向导：

    -   **接受转换规则**

    -   **颁发转换规则**

    -   **颁发授权规则**

    -   **委派授权规则** 
 ![创建规则](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  在 "**选择规则模板**" 页上的 "**声明规则模板**" 下，从列表中选择 "**转换传入声明**"，然后单击 "**下一步**"。
![创建规则](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)

6.  在 "**配置规则**" 页上的 "**声明规则名称**" 下，键入此规则的显示名称。 在 "**传入声明类型**" 中，选择列表中的声明类型。 在 "**传出声明类型**" 中，选择列表中的声明类型，然后选择以下选项之一，这取决于组织的需求：

    -   **传递所有声明值**

    -   **将传入声明值替换为不同的传出声明值**

    -   **将传入电子 \- 邮件后缀声明替换为新的电子 \- 邮件后缀** 
 ![ 创建规则](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform2.PNG)

> [!NOTE]
> 如果要设置使用 AD FS 颁发的声明的动态访问控制方案 \- ，请先在声明提供方信任上创建转换规则，然后在 "**传入声明类型**" 中键入传入声明的名称，或者，如果以前创建了声明说明，请从列表中选择它。 其次，在 "**传出声明类型**" 中选择所需的声明 URL，然后在信赖方信任上创建转换规则以发出设备声明。
>
> 有关动态访问控制方案的详细信息，请参阅[动态访问控制内容路线图](../../solution-guides/dynamic-access-control--scenario-overview.md)或[使用 AD FS AD DS 声明](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831504(v=ws.11))。

7. 单击“完成”。

8. 在 "**编辑声明规则**" 对话框中，单击 **"确定"** 保存规则。

## <a name="additional-references"></a>其他参考
[配置声明规则](Configure-Claim-Rules.md)

[清单：为信赖方信任创建声明规则](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913578(v=ws.11))

[清单：为声明提供方信任创建声明规则](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913564(v=ws.11))

[何时使用授权声明规则](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)

[声明的角色](../../ad-fs/technical-reference/The-Role-of-Claims.md)

[声明规则的角色](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)
