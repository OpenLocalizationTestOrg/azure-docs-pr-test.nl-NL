---
title: aaaConnect virtuele Linux-machines in een cloudservice | Microsoft Docs
description: Verbinding maken met de Hallo classic deployment model tooan Azure-cloudservice of een virtueel netwerk gemaakt virtuele Linux-machines.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 323baf04390d53ffb2810e24a24d175c08e60cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-linux-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Verbinding gemaakt met het klassieke implementatiemodel Hallo met een virtueel netwerk of cloud service virtuele Linux-machines
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Linux virtuele machines is gemaakt met het klassieke implementatiemodel Hallo worden altijd in een cloudservice geplaatst. Hallo cloud-service fungeert als een container en een unieke openbare DNS-naam, een openbare IP-adres en een set eindpunten tooaccess Hallo virtuele machine biedt ten opzichte van Hallo Internet. Hallo-cloudservice kan zich in een virtueel netwerk, maar is geen vereiste. U kunt ook [Windows virtuele machines verbinding met een virtueel netwerk of cloud service](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Als een cloudservice niet in een virtueel netwerk, er sprake een *zelfstandige* cloudservice. Hallo virtuele machines in een zelfstandige cloudservice communiceren met andere virtuele machines met behulp van andere virtuele machines openbare DNS-namen Hallo en Hallo-verkeer verplaatst zich via Internet Hallo. Als een cloudservice in een virtueel netwerk, Hallo virtuele machines is in deze cloudservice met andere virtuele machines in het virtuele netwerk Hallo communiceren kan zonder verkeer verzenden via Internet Hallo.

Als u uw virtuele machines in dezelfde zelfstandige cloudservice hello, kunt u taakverdeling en beschikbaarheidssets. Zie voor meer informatie [taakverdeling van virtuele machines](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en [Hallo beschikbaarheid van virtuele machines beheren](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). U kan echter organiseren Hallo virtuele machines op subnetten of verbinding maken met een zelfstandige cloud service tooyour on-premises netwerk. Hier volgt een voorbeeld:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Volgende stappen
Nadat u een virtuele machine maakt, is het een goed idee te[een gegevensschijf toevoegen](attach-disk.md) zodat uw services en werkbelastingen hebt een locatie toostore gegevens.
