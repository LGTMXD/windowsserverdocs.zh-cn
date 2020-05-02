---
title: tpmtool
description: Tpmtool 的参考主题，用于获取有关受信任的平台模块的信息。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: f2e283dd20d22418416958686d77605976923eaf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721333"
---
# <a name="tpmtool"></a>tpmtool

此实用程序可用于获取有关[受信任的平台模块（TPM）](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview)的信息。

>[!IMPORTANT]
>有些信息与预发布产品相关，这些产品在商业发行之前可能发生重大更改。 Microsoft 对此处提供的信息不提供任何明示或暗示的保证。

有关如何使用此命令的示例，请参阅[示例](#tpmtool_examples)。

## <a name="syntax"></a>语法

```
tpmtool /parameter [<arguments>]
```
### <a name="parameters"></a>参数

|参数|描述|
|---------|-----------|
|getdeviceinformation|显示 TPM 的基本信息。 [此处](https://docs.microsoft.com/windows/desktop/SecProv/win32-tpm-isreadyinformation#parameters)提供信息标志值的含义。|
|gatherlogs [输出目录路径]|收集 TPM 日志，并将其放在指定的目录中。 如果该目录不存在，则创建它。 默认情况下，它们位于当前目录中。 生成的可能文件包括： </br>-TpmEvents .evtx</br>-TpmInformation .txt</br>-SRTMBoot</br>-SRTMResume</br>-DRTMBoot</br>-DRTMResume</br>|
|drivertracing [start/stop]|开始/停止收集 TPM 驱动程序跟踪。 将生成跟踪日志 TPMTRACE，并将其放入当前目录。|
|parsetcglogs [-validate （-v）]|显示已分析的 TCG 日志，也称为 Windows 启动配置日志（WBCL）。 可在[TCG 网站](https://trustedcomputinggroup.org/resource/pc-client-specific-platform-firmware-profile-specification/)上的**事件说明**中找到最新的事件说明。 如果设置`-validate`了标志，则验证 TPM 上的平台配置注册（PCR）值是否与日志中的值匹配。|
|/?|在命令提示符下显示帮助。|

## <a name="examples"></a><a name=tpmtool_examples></a>示例

若要显示 TPM 的基本信息，请键入：
```
tpmtool getdeviceinformation
```
若要收集 TPM 日志并将其放在当前目录中，请键入：
```
tpmtool gatherlogs
```
若要收集 TPM 日志并将其`C:\Users\Public`放入，请键入：
```
tpmtool gatherlogs C:\Users\Public
```
若要收集 TPM 驱动程序跟踪，请键入：
```
tpmtool drivertracing start
# Run scenario
tpmtool drivertracing stop
```
分析 TCG 日志：
```
tpmtool parsetcglogs
```
分析 TCG 日志并验证 PCRs：
```
tpmtool parsetcglogs -validate
```

## <a name="decoding-error-codes"></a>编码错误代码

[此处](https://docs.microsoft.com/windows/desktop/com/com-error-codes-6)介绍了特定于 TPM 的错误代码。
