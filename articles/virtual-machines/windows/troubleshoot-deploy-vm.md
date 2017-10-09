---
title: problemen met Windows virtuele machine in Azure implementeren aaaTroubleshoot | Microsoft Docs
description: Problemen met implementatie Windows virtuele machine in Azurethe Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a>Problemen met implementatie Windows virtuele machine in Azure

tootroubleshoot implementatieproblemen van virtuele machine (VM) in Azure, bekijk Hallo [top problemen](#top-issues) voor algemene fouten en oplossingen.

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.

## <a name="top-issues"></a>Meest voorkomende problemen
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

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

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a>Hoe kan ik gebruiken en de installatiekopie van een windows-client implementeren in Azure?

U kunt Windows 7, Windows 8 of Windows 10 in Azure gebruiken voor ontwikkel-/ Testscenario's als u een juiste Visual Studio (voorheen MSDN)-abonnement hebt. Dit [artikel](client-images.md) overzichten Hallo in aanmerking komt vereisten voor het uitvoeren van Windows-client in Azure en het gebruik van Hallo galerie van Azure-installatiekopieën.

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a>Hoe kan ik een virtuele machine met Hallo hybride gebruik voordeel (HUB) implementeren?

Er zijn een aantal virtuele machines van verschillende manieren toodeploy Windows Hello Azure hybride gebruik Benefit.

Voor een Enterprise Agreement-abonnement:

• VM's van specifieke Marketplace-installatiekopieën die vooraf geconfigureerd met Azure hybride gebruik voordeel zijn implementeren.

Voor Enterprise-overeenkomst:

• Een aangepaste VM uploaden en implementeren met behulp van een Resource Manager-sjabloon of Azure PowerShell.

Zie voor meer informatie Hallo resources te volgen:

 - [Overzicht van Azure hybride gebruik Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [Downloadbare Veelgestelde vragen](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - [Azure hybride gebruik voordeel voor WindowsServer en Windows-Client](hybrid-use-benefit-licensing.md).

 - [Hoe kan ik Hallo hybride gebruiken voordeel gebruiken in Azure](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Hoe kan ik mijn maandelijkse tegoed voor Visual studio Enterprise (BizSpark) activeren

tooactivate uw maandelijkse tegoed, ziet u dit [artikel](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a>Hoe tooadd Enterprise ontwikkelen en testen toomy Enterprise Agreement (EA) tooget tooWindow clientimages toegang?

Hallo mogelijkheid toocreate abonnementen op basis van Hallo Enterprise ontwikkelen en testen bieden is beperkt tooAccount eigenaars die toodo machtiging hebben gekregen in dat geval door een ondernemingsadministrator bent. Hallo accounteigenaar abonnementen via Hallo Portal voor Azure-Account maakt en vervolgens actieve Visual Studio-abonnees moet toevoegen als medebeheerders. Zodat ze kunnen beheren en gebruiken van Hallo-resources die nodig zijn voor het ontwikkelen en testen. Zie voor meer informatie [Enterprise ontwikkelen en testen](https://azure.microsoft.com/offers/ms-azr-0148p/).

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a>De stuurprogramma's ontbreken voor mijn Windows-VM met N-serie

Stuurprogramma's voor Windows-VM's zich bevinden [hier](n-series-driver-setup.md).

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Ik kan een GPU-exemplaar niet vinden in mijn VM N-serie

tootake profiteren van Hallo GPU-mogelijkheden van Azure N-serie VM's met WindowsServer 2016 of Windows Server 2012 R2, moet u NVIDIA grafische stuurprogramma's installeren op elke virtuele machine na de implementatie. Stuurprogramma-installatie-informatie is beschikbaar voor [VM's van Windows](n-series-driver-setup.md) en [virtuele Linux-machines](../linux/n-series-driver-setup.md).

## <a name="are-client-images-supported-for-n-series"></a>Worden de clientinstallatiekopieën van de voor N-serie ondersteund?

Azure ondersteunt momenteel alleen N-reeks op virtuele machines met Windows Server- en Linux-besturingssystemen.

## <a name="is-n-series-vms-available-in-my-region"></a>Virtuele machines N-reeks is beschikbaar in mijn regio?

U kunt controleren Hallo beschikbaarheid van Hallo [producten die per regio tabel](https://azure.microsoft.com/regions/services), en prijzen [hier](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a>Welke clientimages kan ik gebruiken en te implementeren in Azure, en hoe tooI ze?

U kunt Windows 7, Windows 8 of Windows 10 in Azure voor ontwikkel-/ Testscenario's geleverde dat een juiste Visual Studio (voorheen MSDN)-abonnement hebt. 

- Installatiekopieën van Windows 10 zijn beschikbaar in de galerie van Azure Hallo binnen [in aanmerking komende ontwikkelen en testen biedt](client-images.md#eligible-offers). 
- Visual Studio-abonnees binnen elk type aanbieding kunnen ook [voldoende voorbereiden en maken](prepare-for-upload-vhd-image.md) een 64-bits installatiekopie voor Windows 7, Windows 8 of Windows 10 en vervolgens [tooAzure uploaden](upload-generalized-managed.md). Hallo gebruik blijft beperkt toodev en testen door actieve Visual Studio-abonnees.

Dit [artikel](client-images.md) overzichten Hallo in aanmerking komt vereisten voor het uitvoeren van Windows-client in Azure en het gebruik van Hallo galerie van Azure-installatiekopieën.

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Ik wil niet kunnen toosee VM-grootte familie die ik wil wanneer het formaat van mijn VM.

Wanneer een virtuele machine wordt uitgevoerd, is het geïmplementeerde tooa fysieke server. Hallo fysieke servers in de Azure-regio's worden gegroepeerd in clusters van algemene fysieke hardware. Formaat van een virtuele machine waarvoor Hallo VM toobe verplaatst toodifferent hardware clusters verschilt, afhankelijk van welke implementatiemodel gebruikte toodeploy Hallo VM is.

- Virtuele machines die worden geïmplementeerd in het klassieke implementatiemodel, Hallo cloud service-implementatie moeten worden verwijderd en opnieuw geïmplementeerd toochange Hallo VMs tooa grootte in een ander grootte gezin.

- Virtuele machines in de Resource Manager-implementatiemodel zijn geïmplementeerd, moet u alle virtuele machines stoppen in Hallo beschikbaarheidsset voordat u de grootte van een virtuele machine in de beschikbaarheidsset Hallo Hallo wijzigt.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Hallo wordt vermelde VM-grootte niet ondersteund tijdens de implementatie in Beschikbaarheidsset.

Kies een grootte die wordt ondersteund op Hallo beschikbaarheidsset-cluster. Het wordt aanbevolen bij het maken van dat een beschikbaarheidsset toochoose Hallo VM maximumgrootte u denkt dat u nodig hebt en u hebt uw eerste implementatie toohello beschikbaarheidsset worden.

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Kan ik een bestaande beschikbaarheidsset voor klassieke VM tooan toevoegen?

Ja. U kunt een bestaande klassieke VM tooa nieuwe toevoegen of bestaande Beschikbaarheidsset. Zie voor meer informatie [toevoegen van een bestaande beschikbaarheidsset voor de virtuele machine tooan](classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Volgende stappen
Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/).

U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.
