---
title: een klassieke virtuele Linux-machine met aaaCreate hello Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe een virtuele Linux-machine met het gebruik van Azure CLI 1.0 Hallo toocreate Hallo klassieke implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>Hoe tooCreate een klassieke Linux-VM met Azure CLI 1.0 Hallo
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor de Resource Manager-versie Hallo [hier](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Dit onderwerp wordt beschreven hoe toocreate virtuele Linux-machine (VM) met het gebruik van Azure CLI 1.0 Hallo Hallo klassieke implementatiemodel. We gebruiken de installatiekopie van een Linux van Hallo beschikbaar **INSTALLATIEKOPIEËN** op Azure. Hello Azure CLI 1.0 opdrachten geven Hallo na configuratie-opties, onder andere:

* Hallo VM tooa virtueel netwerk verbinden
* Hallo VM tooan bestaande cloudservice toevoegen
* Hallo VM tooan bestaande opslagaccount toevoegen
* Hallo VM tooan beschikbaarheidsset of locatie toe te voegen

> [!IMPORTANT]
> Als u uw VM toouse een virtueel netwerk, wilt zodat u verbinding met tooit rechtstreeks door de hostnaam of het instellen van de cross-premises verbindingen maken kunt, zorg er dan voor dat u opgeeft Hallo virtueel netwerk wanneer u Hallo VM maakt. Een virtuele machine kan geconfigureerde toojoin een virtueel netwerk worden alleen wanneer u Hallo VM maakt. Zie voor meer informatie over virtuele netwerken, [Azure Virtual Network-overzicht](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>Hoe toocreate een Linux-VM met Hallo klassieke implementatiemodel
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

