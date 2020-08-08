---
title: AD FS 故障排除-Idp-启动的登录
description: 本文档介绍如何排查 AD FS 登录页的问题。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: 4eb39b697b3dd31dc0a6e3581bdb33437b462197
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969704"
---
# <a name="ad-fs-troubleshooting---idp-initiated-sign-on"></a>AD FS 故障排除-Idp-启动的登录
AD FS 登录页可用于测试身份验证是否正常工作。  这是通过导航到页面并登录来完成的。  此外，我们还可以使用登录页验证是否列出了所有 SAML 2.0 信赖方。

## <a name="enable-the-idp-initiated-sign-on-page"></a>启用 Idp 启动的登录页
默认情况下，Windows 2016 中的 AD FS 未启用登录页。  若要启用此设置，可以使用 PowerShell 命令 Set-adfsproperties。  使用以下过程来启用该页：

1.  打开 Windows PowerShell
2.  输入： `Get-AdfsProperties` ，然后按 enter
3.  验证**EnableIdpInitiatedSignonPage**设置为 false ![ false](media/ad-fs-tshoot-initiatedsignon/idp2.png)
4.  在 PowerShell 中，输入：`Set-AdfsProperties -EnableIdpInitiatedSignonPage $true`
5.  你将看不到确认，因此请再次输入 Set-adfsproperties 并确认**EnableIdpInitatedSignonPage**设置为 true。
![True](media/ad-fs-tshoot-initiatedsignon/idp4.png)

## <a name="test-authentication"></a>测试身份验证
使用以下过程，通过 Idp 启动的登录页测试 AD FS 身份验证。

1.  打开 web 浏览器并导航到 Idp 登录页。  示例：https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
2.  系统将提示你登录。  输入凭据。
![登录](media/ad-fs-tshoot-initiatedsignon/idp5.png)
3.  如果此操作成功，您应该登录。


## <a name="test-authentication-using-a-seamless-logon-experience"></a>使用无缝登录体验测试身份验证
可以通过确保将 AD FS 服务器的 URL 添加到 internet 选项的 "本地 intranet" 区域来测试无缝登录体验。  请按以下过程操作：

1.  在 Windows 10 客户端上，单击 "开始" 并键入 "internet 选项"，然后选择 "internet 选项"。
2.   单击 "安全" 选项卡，单击 "本地 intranet"，然后单击 "站点" 按钮。
![无缝](media/ad-fs-tshoot-initiatedsignon/idp8.png)
1.  单击“高级”。
2.  输入 url，并单击 "添加"。  单击“关闭”。
![添加 url](media/ad-fs-tshoot-initiatedsignon/idp9.png)
1.  单击“确定”。  单击“确定”。  这应该会关闭 "internet 选项"。
2.  打开 web 浏览器并导航到 Idp 登录页。  示例：https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
3.  单击 "登录" 按钮。  应该会自动登录，而不会提示输入凭据。
![无缝](media/ad-fs-tshoot-initiatedsignon/idp6.png)

## <a name="next-steps"></a>后续步骤

- [AD FS 疑难解答](ad-fs-tshoot-overview.md)
