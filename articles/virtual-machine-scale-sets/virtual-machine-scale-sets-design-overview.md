---
title: Overwegingen voor Azure Virtual Machine-Schaalsets aaaDesign | Microsoft Docs
description: Meer informatie over overwegingen bij het ontwerpen voor uw Azure virtuele-Machineschaalsets
keywords: virtuele Linux-machine, virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>Ontwerpoverwegingen voor Schaalsets
Dit onderwerp wordt besproken ontwerpoverwegingen voor het virtuele-Machineschaalsets. Voor informatie over wat virtuele-Machineschaalsets zijn, Raadpleeg te[overzicht van virtuele machines Scale Sets](virtual-machine-scale-sets-overview.md).

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>Wanneer toouse scale Hiermee stelt u in plaats van virtuele machines?
In het algemeen zijn schaalsets nuttig voor het implementeren van maximaal beschikbare infrastructuur waarin een set machines vergelijkbare configuratie hebben. Sommige functies zijn echter alleen beschikbaar in schaalsets terwijl andere functies alleen beschikbaar in virtuele machines zijn. In volgorde toomake een gefundeerde beslissing nemen over wanneer toouse elke technologie we moeten eerst eens kijken aantal Hallo gebruikte functies die beschikbaar in-schaalsets, maar geen virtuele machines zijn:

### <a name="scale-set-specific-features"></a>Scale set-specifieke functies

- Zodra u Hallo scale set configuratie opgeeft, kunt u gewoon bijwerken Hallo 'capaciteit' eigenschap toodeploy meer virtuele machines parallel. Dit is veel eenvoudiger dan het schrijven van een script tooorchestrate veel afzonderlijke VM's parallel te implementeren.
- U kunt [gebruik Azure automatisch schalen tooautomatically schalen een schaalset](./virtual-machine-scale-sets-autoscale-overview.md) maar geen afzonderlijke virtuele machines.
- U kunt [terugzetten van de installatiekopie schaalset VMs](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm) maar [geen afzonderlijke virtuele machines](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- U kunt [overprovision](./virtual-machine-scale-sets-design-overview.md) schaalset virtuele machines voor grotere betrouwbaarheid en sneller implementatietijden. U doen dit niet met afzonderlijke virtuele machines tenzij u aangepaste code toodo dit schrijven.
- Kunt u een [Upgradebeleid](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake het eenvoudig tooroll upgrades over VM's in de schaalset uitvoeren. Met afzonderlijke virtuele machines, u moet u updates indeelt zelf.

### <a name="vm-specific-features"></a>VM-specifieke functies

Op Hallo daarentegen, sommige functies zijn alleen beschikbaar in virtuele machines (ten minste voor Hallo tijd):

- U kunt gegevens schijven toospecific bijvoegen afzonderlijke virtuele machines, maar de gegevensschijven van de gekoppelde zijn geconfigureerd voor alle VM's in een schaalset.
- U kunt gegevens van niet-lege schijven tooindividual VM's, maar geen virtuele machines in een schaalset koppelen.
- U kunt een momentopname van een afzonderlijke VM, maar niet een virtuele machine in een schaalset.
- U kunt een installatiekopie van een afzonderlijke virtuele machine, maar niet op een virtuele machine in een set scale vastleggen.
- U kunt een afzonderlijke virtuele machine migreren van systeemeigen schijven toomanaged schijven, maar kan geen u dit doen voor virtuele machines in een schaalset.
- U IPv6-openbare IP-adressen tooindividual VM NIC's kunt toewijzen, maar niet voor virtuele machines in een schaalset. Houd er rekening mee dat u het openbare IP-adressen IPv6 tooload balancers voor een afzonderlijke virtuele machines toewijzen kunt of VM-schaalset.

## <a name="storage"></a>Storage

### <a name="scale-sets-with-azure-managed-disks"></a>Schaalsets met beheerde Azure-schijven
Schaalsets kunnen worden gemaakt met [Azure beheerd schijven](../virtual-machines/windows/managed-disks-overview.md) in plaats van traditionele Azure storage-accounts. Beheerde schijven bieden Hallo volgende voordelen:
- U hebt geen toopre-maken van een set van Azure storage-accounts voor Hallo virtuele machines schaalset.
- U kunt definiëren [gegevensschijven gekoppeld](virtual-machine-scale-sets-attached-disks.md) voor Hallo VM's in uw scale ingesteld.
- -Schaalsets te kunnen worden geconfigureerd[ondersteuning voor maximaal too1, 000 VM's in een set](virtual-machine-scale-sets-placement-groups.md). 

Als u een bestaande sjabloon hebt, kunt u ook [bijwerken Hallo sjabloon toouse beheerde schijven](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Opslag gebruikers wordt beheerd
Een schaalset die niet is gedefinieerd met Azure beheerd schijven afhankelijk van de gebruiker gemaakte accounts toostore Hallo OS opslagschijven Hallo VM's in Hallo set. Een ratio van 20 VM's per storage-account of minder wordt aanbevolen tooachieve maximale i/o en ook profiteren van de _overmatige inrichting_ (Zie hieronder). Het is ook raadzaam dat u Hallo begin tekens van de namen van opslagaccounts Hallo verdeeld over Hallo alfabet. Dit doet, helpt load verdeeld over verschillende interne systemen. 


## <a name="overprovisioning"></a>Overmatige inrichting
Schaal stelt momenteel standaard te 'overmatige inrichting' virtuele machines. Met overmatige inrichting ingeschakeld, Hallo scale daadwerkelijk draaien om zo meer VM's dan u om hebt gevraagd instellen en vervolgens verwijdert Hallo extra VM's wanneer Hallo aangevraagd aantal virtuele machines met succes zijn ingericht. Overmatige inrichting verbetert inrichting succespercentages en minder implementatietijd. U wordt niet voor hello extra VM's, en ze niet voor uw quotalimieten meetellen gefactureerd.

Terwijl overmatige inrichting inrichting succespercentages verbeteren, kan dit leiden tot verwarring gedrag voor een toepassing die is niet ontworpen toohandle extra VM's die wordt weergegeven en klik vervolgens verdwijnen. tooturn overmatige inrichting uitgeschakeld, Controleer of er Hallo tekenreeks in de sjabloon te volgen: `"overprovision": "false"`. Meer informatie vindt u in Hallo [Scale ingesteld REST API-documentatie](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Als uw scale set gebruikers wordt beheerd opslag gebruikt en u overmatige inrichting uitschakelen, kunt u meer dan 20 VM's per storage-account hebben, maar het wordt niet aangeraden toogo hierboven 40 van de i/o-prestaties. 

## <a name="limits"></a>Limieten
Een schaalset gebouwd op een Marketplace-installatiekopie (ook wel bekend als een platforminstallatiekopie) en Azure beheerd schijven een capaciteit van up too1, 000 VMs ondersteunt toouse geconfigureerd. Als u uw scale set toosupport meer dan 100 virtuele machines configureert, niet alle scenario's werken dezelfde Hallo (voor een voorbeeld van de taakverdeling). Zie voor meer informatie [werken met grote virtuele machine-schaalsets](virtual-machine-scale-sets-placement-groups.md). 

Een schalen instellen met gebruikers wordt beheerd storage-accounts geconfigureerd is momenteel beperkt too100 VMs (en 5 storage-accounts worden aanbevolen voor deze schaal).

Een schaalset gebouwd op een aangepaste installatiekopie (één gebouwd door u) kan een capaciteit van up too100 VM's wanneer geconfigureerd met Azure-beheerde schijven hebben. Als Hallo scale set wordt geconfigureerd met gebruikers wordt beheerd storage-accounts, moet deze alle OS VHD's van schijf binnen een opslagaccount maken. Als gevolg hiervan Hallo maximale aanbevolen aantal virtuele machines in een set scale is gebouwd op een aangepaste installatiekopie en gebruikers wordt beheerd opslag is 20. Als u overmatige inrichting uitschakelt, kunt u up too40 gaan.

Voor meer virtuele machines dan deze limiet is toegestaan, moet u meerdere scale ingesteld zoals wordt weergegeven in toodeploy [deze sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

