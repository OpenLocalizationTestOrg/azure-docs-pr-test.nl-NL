---
title: problemen met Linux virtuele machine in Azure implementeren aaaTroubleshoot | Microsoft Docs
description: Problemen met implementatie Linux virtuele machine in Azurethe Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Problemen met implementatie Linux virtuele machine in Azure

tootroubleshoot implementatieproblemen van virtuele machine (VM) in Azure, bekijk Hallo [top problemen](#top-issues) voor algemene fouten en oplossingen.

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.

## <a name="top-issues"></a>Meest voorkomende problemen
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>Hallo-cluster kan niet ondersteunen Hallo aangevraagde VM-grootte
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Probeer Hallo-aanvraag met een kleinere VM.
- Als hello aangevraagde grootte van Hallo dat VM kan niet worden gewijzigd:
    - Stop alle Hallo-VM's in de beschikbaarheidsset Hallo. Klik op **resourcegroepen** > uw resourcegroep > **Resources** > uw beschikbaarheidsset > **virtuele Machines** > uw virtuele machine >  **Stop**.
    - Nadat alle virtuele machines stoppen Hallo, Hallo VM maken in Hallo gewenst grootte.
    - Start eerst Hallo van nieuwe virtuele machine en vervolgens Selecteer Hallo gestopt VM's en klik op Start.


## <a name="hello-cluster-does-not-have-free-resources"></a>Hallo-cluster heeft geen gratis resources
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Hallo aanvraag later opnieuw proberen.
- Als hello nieuwe virtuele machine kan deel uitmaken van een andere beschikbaarheidsset instellen
    - Een virtuele machine maken in een andere beschikbaarheidsset (in Hallo dezelfde regio).
    - Toevoegen van nieuwe VM-toohello Hallo hetzelfde virtuele netwerk.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Hoe kan ik mijn maandelijkse tegoed voor Visual studio Enterprise (BizSpark) activeren

tooactivate uw maandelijkse tegoed, ziet u dit [artikel](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>Waarom kan ik Hallo GPU-stuurprogramma niet voor een virtuele Ubuntu-machine NV installeren?

Linux GPU-ondersteuning is momenteel alleen beschikbaar op Azure NC Virtual machines Ubuntu Server 16.04 TNS uitgevoerd. Zie voor meer informatie [GPU-stuurprogramma's instellen voor N-reeks virtuele machines met Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>De stuurprogramma's ontbreken voor mijn Linux-VM met N-serie

Stuurprogramma's voor op basis van Linux virtuele machines zich bevinden [hier](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Ik kan een GPU-exemplaar niet vinden in mijn VM N-serie

tootake profiteren van Hallo GPU-mogelijkheden van Azure N-serie VM's met WindowsServer 2016 of Windows Server 2012 R2, moet u NVIDIA grafische stuurprogramma's installeren op elke virtuele machine na de implementatie. Stuurprogramma-installatie-informatie is beschikbaar voor [VM's van Windows](../windows/n-series-driver-setup.md) en [virtuele Linux-machines](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>Virtuele machines N-reeks is beschikbaar in mijn regio?

U kunt controleren Hallo beschikbaarheid van Hallo [producten die per regio tabel](https://azure.microsoft.com/regions/services), en prijzen [hier](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Ik wil niet kunnen toosee VM-grootte familie die ik wil wanneer het formaat van mijn VM.

Wanneer een virtuele machine wordt uitgevoerd, is het geïmplementeerde tooa fysieke server. Hallo fysieke servers in de Azure-regio's worden gegroepeerd in clusters van algemene fysieke hardware. Formaat van een virtuele machine waarvoor Hallo VM toobe verplaatst toodifferent hardware clusters verschilt, afhankelijk van welke implementatiemodel gebruikte toodeploy Hallo VM is.

- Virtuele machines die worden geïmplementeerd in het klassieke implementatiemodel, Hallo cloud service-implementatie moeten worden verwijderd en opnieuw geïmplementeerd toochange Hallo VMs tooa grootte in een ander grootte gezin.

- Virtuele machines in de Resource Manager-implementatiemodel zijn geïmplementeerd, moet u alle virtuele machines stoppen in Hallo beschikbaarheidsset voordat u de grootte van een virtuele machine in de beschikbaarheidsset Hallo Hallo wijzigt.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Hallo wordt vermelde VM-grootte niet ondersteund tijdens de implementatie in Beschikbaarheidsset.

Kies een grootte die wordt ondersteund op Hallo beschikbaarheidsset-cluster. Het wordt aanbevolen bij het maken van dat een beschikbaarheidsset toochoose Hallo VM maximumgrootte u denkt dat u nodig hebt en u hebt uw eerste implementatie toohello beschikbaarheidsset worden.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Welke Linux-distributies/versies worden ondersteund in Azure?

U kunt de lijst Hallo op Linux vinden op [Azure-Endorsed distributies](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Kan ik een bestaande beschikbaarheidsset voor klassieke VM tooan toevoegen?

Ja. U kunt een bestaande klassieke VM tooa nieuwe toevoegen of bestaande Beschikbaarheidsset. Zie voor meer informatie [toevoegen van een bestaande beschikbaarheidsset voor de virtuele machine tooan](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Volgende stappen
Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/).

U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.
