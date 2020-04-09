---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: 添加令牌解密证书
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5714a41950b9c2f818ddc154a9af7a55fdb362d8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814961"
---
# <a name="add-a-token-decrypting-certificate"></a>添加令牌解密证书

在将新的证书设置为主解密证书后，如果信赖方联合服务器必须对使用较旧证书颁发的令牌进行解密，联合服务器将使用令牌\-解密证书。 Active Directory 联合身份验证服务 \(AD FS\) 使用安全套接字层 \(\) Internet Information Services \(\) 证书作为默认的解密证书。  
  
> [!CAUTION]  
> 用于令牌\-解密的证书对联合身份验证服务稳定性至关重要。 由于为此目的配置的任何证书丢失或未计划删除都可能中断服务，因此应备份任何为此目的配置的证书。  
  
你可以使用以下过程将令牌\-解密证书添加到中的 "AD FS 管理" 管理单元\-中。  
  
若要完成此过程，至少需要是本地计算机上的**管理员**组或等效组中的成员。  有关使用适当帐户和组成员身份的详细信息，请参阅[本地和域默认组](https://go.microsoft.com/fwlink/?LinkId=83477)\(http：\/\/go.microsoft.com\/fwlink\/？LinkId\=83477\)。   
  
### <a name="to-add-a-token-decrypting-certificate"></a>\-解密证书添加令牌  
  
1.  在 "**开始**" 屏幕上，键入 "**AD FS 管理**"，然后按 enter。  
  
2.  在控制台树中，\-双击 "**服务**"，然后单击 "**证书**"。  
  
3.  在 "**操作**" 窗格中，单击 "**添加令牌\-解密证书**" 链接。  
  
4.  在 "**浏览证书文件**" 对话框中，导航到要添加的证书文件，选择证书文件，然后单击 "**打开**"。  
  
## <a name="additional-references"></a>其他参考  
[清单：设置联合服务器](Checklist--Setting-Up-a-Federation-Server.md)  
  
[联合服务器的证书要求](https://technet.microsoft.com/library/dd807040.aspx)  
  

