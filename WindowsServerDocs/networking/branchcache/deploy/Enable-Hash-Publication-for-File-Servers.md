---
title: 启用文件服务器的哈希发布
description: 本主题是适用于 Windows Server 2016 的 BranchCache 部署指南的一部分，它演示了如何在分布式和托管缓存模式下部署 BranchCache，以优化分支机构中的 WAN 带宽使用情况
manager: brianlic
ms.topic: get-started-article
ms.assetid: 5697aefe-1dd2-4ff9-82a9-da0afc182cb3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 405fe3ea4d7afc771c65442483b1660916aa8d4c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971844"
---
# <a name="enable-hash-publication-for-file-servers"></a>启用文件服务器的哈希发布

>适用于：Windows Server（半年频道）、Windows Server 2016

可以在一个文件服务器或多个文件服务器上启用 BranchCache 哈希发布。

-   若要使用本地计算机组策略在一台文件服务器上启用哈希发布，请参阅[为非域成员文件服务器启用哈希发布](../../branchcache/deploy/Enable-Hash-Publication-for-Non-Domain-Member-File-Servers.md)。

-   若要在使用域组策略的多个文件服务器上启用哈希发布，请参阅[为域成员文件服务器启用哈希发布](../../branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)。

> [!NOTE]
> 如果你有多个文件服务器，并且想要为每个共享启用哈希发布，而不是对所有共享启用哈希发布，则可以使用主题[为非域成员文件服务器启用哈希发布](Enable-Hash-Publication-for-Non-Domain-Member-File-Servers.md)主题中的说明。



