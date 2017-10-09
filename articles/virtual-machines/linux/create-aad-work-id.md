---
title: een werk- of schoolaccount-id in van AAD voor Linux aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een werk- of schoolaccount-id in Azure Active Directory-toouse met uw virtuele Linux-machines.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a>Maken van een identiteit werk of School in Azure Active Directory-toouse met Linux VM 's
Als u een persoonlijke Azure-account gemaakt of een persoonlijke MSDN-abonnement hebt en hello Azure-account tootake profiteren van de MSDN-Azure-tegoed met Hallo--gemaakt die u gebruikt een *Microsoft-account* identiteit toocreate deze. Veel grote voordelen van Azure-- [resource groep sjablonen](../../azure-resource-manager/resource-group-overview.md) is een voorbeeld--vereisen een account (een identiteit die wordt beheerd door Azure Active Directory) met het werk of school toowork. U kunt instructies Hallo hieronder toocreate dat een nieuwe werk of school-account omdat gelukkig Hallo best bewerkingen over uw persoonlijke Azure-account dat wordt geleverd met een standaard Azure Active Directory-domein dat u toocreate kunt een nieuwe werk of school account dat u kunt gebruiken met Azure-functies waarvoor dit is vereist.

Echter, recente wijzigingen maken het mogelijk toomanage uw abonnement met een Azure-account met behulp van Hallo `azure login` beschreven methode voor interactieve aanmelding [hier](../../xplat-cli-connect.md). U kunt dit mechanisme gebruiken of kunt u Hallo instructies volgen. U kunt ook [een werk- of schoolaccount-id maakt in Azure Active Directory-toouse met VM's van Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

