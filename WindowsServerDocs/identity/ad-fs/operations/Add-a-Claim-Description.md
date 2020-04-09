---
ms.assetid: 7d230527-f4fe-4572-8838-0b354ee0b06b
title: 添加声明说明
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9c5293dc6070c9483054ce1dd827a20ec377573b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859710"
---
# <a name="add-a-claim-description"></a>添加声明说明


在帐户伙伴组织中，管理员创建声明来表示用户在组或角色中的成员身份，或表示有关用户的一些数据，例如，用户的员工标识号。

在资源伙伴组织中，管理员创建相应的声明来表示可被识别为资源用户的组和用户。 因为帐户伙伴组织中的传出声明映射到资源伙伴组织中的传入声明，资源伙伴可以接受帐户伙伴提供的凭据。 

你可以使用以下过程添加声明。

若要完成此过程，至少需要是本地计算机上的**管理员**组或等效组中的成员。  可在[本地默认组和域默认组](https://go.microsoft.com/fwlink/?LinkId=83477)中查看有关使用适合的帐户和组成员身份的详细信息。

## <a name="to-add-a-claim-description"></a>添加声明说明

1. 在服务器管理器中，单击 "**工具**"，然后选择 " **AD FS 管理**"。 

2. 展开 "**服务**"，然后在右侧单击 "**添加声明说明**"。
   ![添加声明说明](media/Add-a-Claim-Description/claimdesc1.png)

3. 在 "添加声明说明" 对话框中的 "**显示名称**" 中，键入标识此声明的组或角色的唯一名称。

4. 添加**短名称**。

5. 在 "**声明标识符**" 中，键入与将使用的声明的组或角色关联的 URI。

6. 在 "**说明**" 下，键入最能说明此声明用途的文本。

7. 根据组织的需要，根据需要选中以下复选框之一，将此声明发布到联合元数据中：


~~~
- To publish this claim to make partners aware that this server can accept this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can accept**.
- To publish this claim to make partners aware that this server can issue this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can send**.
~~~

8. 单击“确定”。

![添加声明说明](media/Add-a-Claim-Description/claimdesc2.png)


## <a name="see-also"></a>另请参阅  
[AD FS 操作](../../ad-fs/AD-FS-2016-Operations.md) 
