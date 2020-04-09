---
title: secedit：配置
description: 适用于 * * * * 的 Windows 命令主题
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a92e68ca-003c-4219-8655-0e7734f5fab3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 288886b486052fea62c7b89758890a664e1da0ce
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834980"
---
# <a name="seceditconfigure"></a>secedit：配置



允许使用数据库中存储的安全设置来配置当前系统设置。 有关如何使用此命令的示例，请参阅[示例](#BKMK_Examples)。

## <a name="syntax"></a>语法

```
Secedit /configure /db <database file name> [/cfg <configuration file name>] [/overwrite] [/areas SECURITYPOLICY | GROUP_MGMT | USER_RIGHTS | REGKEYS | FILESTORE | SERVICES] [/log <log file name>] [/quiet]
```

#### <a name="parameters"></a>参数

|参数|说明|
|---------|-----------|
|db|必需。</br>指定包含存储配置的数据库的路径和文件名。</br>如果文件名指定的数据库不具有与其关联的安全模板（由配置文件表示），则还必须指定 `/cfg \<configuration file name>` 命令行选项。|
|cfg|可选。</br>指定将导入到数据库中进行分析的安全模板的路径和文件名。</br>此/cfg 选项仅在与 `/db \<database file name>` 参数一起使用时才有效。 如果未指定此项，则对已存储在数据库中的任何配置执行分析。|
|overwrite|可选。</br>指定/cfg 参数中的安全模板是否应覆盖数据库中存储的任何模板或复合模板，而不是将结果追加到存储的模板。</br>此命令行选项仅在使用 `/cfg \<configuration file name>` 参数时有效。 如果未指定此参数，则将/cfg 参数中的模板追加到存储的模板。|
|区域|可选。</br>指定要应用于系统的安全区域。 如果未指定此参数，则会将数据库中定义的所有安全设置应用到系统。 若要配置多个区域，请用空格分隔每个区域。 支持以下安全区域：</br>-Ws-securitypolicy</br>    系统的本地策略和域策略，包括帐户策略、审核策略、安全选项等。</br>-Group_Mgmt</br>    在安全模板中指定的任何组的限制组设置。</br>-User_Rights</br>    用户登录权限和授予权限。</br>- RegKeys</br>    本地注册表项的安全性。</br>-%</br>    本地文件存储的安全性。</br>-服务</br>    所有已定义服务的安全性。|
|log|可选。</br>指定进程的日志文件的路径和文件名。|
|低温|可选。</br>禁止显示屏幕和日志输出。 你仍可以使用 Microsoft 管理控制台（MMC）的 "安全配置和分析" 管理单元查看分析结果。|

## <a name="remarks"></a>备注

如果未提供日志文件的路径，则使用默认的日志文件（*systemroot*\Users \*用户帐户<em>\My Documents\Security\Logs\*DatabaseName</em>）。

从 Windows Server 2008 开始，`Secedit /refreshpolicy` 已替换为 `gpupdate`。 有关如何刷新安全设置的信息，请参阅[Gpupdate](gpupdate.md)。

## <a name="examples"></a><a name=BKMK_Examples></a>示例

对安全数据库 SecDbContoso （使用 "安全配置和分析" 管理单元创建）的安全参数执行分析。 通过提示将输出定向到文件 SecAnalysisContosoFY11，以便可以验证命令是否正常运行。
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
假设分析显示了一些 inadequacies，因此修改了安全模板 SecContoso。 再次运行该命令以合并更改，将输出定向到现有文件 SecAnalysisContosoFY11，而不会出现提示。
```
Secedit /configure /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

## <a name="additional-references"></a>其他参考

-   [Secedit](secedit.md)
-   [Secedit:analyze](secedit-analyze.md)
-   - [命令行语法项](command-line-syntax-key.md)