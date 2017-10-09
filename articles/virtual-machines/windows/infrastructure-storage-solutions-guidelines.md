---
title: aaaStorage oplossingen voor Windows-machines in Azure | Microsoft Docs
description: Informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor het implementeren van opslagoplossingen voor in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57c27a7305964a56e6b2d1e73dee8e7da19fa8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a>Azure-opslag-infrastructuur richtlijnen voor het Windows-VM 's

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het inzicht opslagbehoeften en overwegingen voor het bereiken van de prestaties van de optimale virtuele machine (VM).

## <a name="implementation-guidelines-for-storage"></a>Implementatie van richtlijnen voor opslag
Beslissingen te nemen:

* Gaat u toouse beheerde Azure-schijven of niet-beheerde schijven?
* Hebt u toouse Standard of Premium-opslag voor de werkbelasting nodig?
* U moet schijf striping toocreate schijven groter is dan 4TB?
* Hebt u striping tooachieve optimale i/o-prestaties van de schijf voor de werkbelasting nodig?
* Welke set van storage-accounts moet u toohost infrastructuur of uw IT-werkbelasting?

Taken:

* Bekijk de i/o-vereisten van Hallo toepassingen die u implementeert en plannen Hallo juiste aantal en type van de storage-accounts.
* Hallo set met behulp van de naamconventie storage-accounts maken. U kunt Azure PowerShell of Hallo portal gebruiken.

## <a name="storage"></a>Storage
Azure Storage is een belangrijk onderdeel van het implementeren en beheren van virtuele machines (VM's) en toepassingen. Azure Storage biedt services voor het opslaan van gegevens uit een bestand, niet-gestructureerde gegevens en berichten, en het is ook deel uit van Hallo-infrastructuur ondersteuning van virtuele machines.

[Azure-beheerde schijven](../../storage/storage-managed-disks-overview.md) opslag voor u achter de schermen Hallo verwerkt. Met niet-beheerde schijven maakt u opslagaccounts toohold Hallo-schijven (VHD-bestanden) voor uw Azure VM's. Wanneer het omhoog schalen, moet u ervoor zorgen dat u extra opslagaccounts hebt gemaakt, zodat u niet Hallo IOP's voor opslag met een van uw schijven overschrijden. Met beheerde schijven afhandeling van opslag, u zijn niet langer beperkt door Hallo opslagaccountlimieten (zoals 20.000 IOPS / -account). Ook niet langer hebt toocopy uw aangepaste installatiekopieën (VHD-bestanden) toomultiple storage-accounts. U kunt deze op een centrale locatie – één opslagaccount per Azure-regio – beheren en gebruiken ze toocreate honderden van virtuele machines in een abonnement. U wordt aangeraden dat u beheerd schijven gebruiken voor nieuwe implementaties.

Er zijn twee soorten storage-accounts beschikbaar ter ondersteuning van virtuele machines:

* Standard-opslag-accounts u bent gemachtigd tooblob opslag (gebruikt voor het opslaan van de virtuele machine van Azure-schijven), storage, queue storage, table en bestandsopslag.
* [Premium-opslag](../../storage/storage-premium-storage.md) accounts bieden ondersteuning voor schijven voor hoge prestaties, lage latentie voor i/o-intensieve werkbelastingen, zoals SQL-Servers in een AlwaysOn-cluster. Premium-opslag ondersteunt momenteel alleen Azure VM-schijven.

Azure maakt virtuele machines met een besturingssysteemschijf, een tijdelijke schijf en nul of meer optionele gegevensschijven. Hallo besturingssysteemschijf en gegevensschijven zijn Azure-pagina-blobs, terwijl de tijdelijke schijf Hallo lokaal wordt opgeslagen op Hallo knooppunt waar de machine Hallo woont. Wees voorzichtig bij het ontwerpen van toepassingen tooonly deze tijdelijke schijf voor niet-permanente gegevens gebruiken als Hallo VM kan worden gemigreerd tussen hosts tijdens onderhoud. Gegevens die zijn opgeslagen op Hallo tijdelijke schijf zou verloren zijn.

Duurzaamheid en maximale beschikbaarheid wordt verstrekt door Hallo onderliggende Azure Storage-omgeving tooensure blijven uw gegevens beveiligen tegen niet-gepland onderhoud of hardwarestoringen. Als u uw Azure Storage-omgeving ontwerpt, kunt u tooreplicate VM-opslag:

* lokaal binnen een bepaald Azure-datacenter
* over Azure-datacenters binnen een bepaald gebied
* over Azure-datacenters over verschillende regio 's

U kunt lezen [meer informatie over opties voor hoge beschikbaarheid voor de replicatie Hallo](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Besturingssysteem-schijven en gegevensschijven hebben een maximale grootte van 4TB. U kunt opslagruimten in Windows Server 2012 of hoger toosurpass deze limiet door het groeperen van schijven toopresent logische gegevensvolumes groter is dan 4TB tooyour VM.

Er zijn bepaalde limieten voor schaalbaarheid bij het ontwerpen van uw implementaties van Azure Storage - voor meer informatie, Zie [Microsoft Azure-abonnement en service-limieten, quota's en beperkingen](../../azure-subscription-service-limits.md#storage-limits). Zie ook [Azure storage schaalbaarheids- en prestatiedoelen](../../storage/storage-scalability-targets.md).

Voor de toepassingsopslag van, kunt u opslaan ongestructureerde objectgegevens, zoals documenten, afbeeldingen, back-ups, configuratiegegevens, Logboeken, enzovoort. met behulp van blob-opslag. In plaats van uw toepassing schrijven tooa virtuele schijf die is gekoppeld toohello VM kunt Hallo-toepassing schrijven rechtstreeks tooAzure blob-opslag. BLOB-opslag biedt ook de optie Hallo van [hot en cool opslaglagen](../../storage/storage-blob-storage-tiers.md) afhankelijk van uw behoeften van de beschikbaarheid en kostenbeperkingen.

## <a name="striped-disks"></a>Striped schijven
Naast het zodat u toocreate schijven groter is dan 4TB in veel gevallen, verbetert met behulp van striping voor gegevensschijven de prestaties doordat meerdere blobs tooback hello opslag voor één volume. Met striping, Hallo i/o toowrite vereist en gelezen gegevens van één logische schijf verloopt parallel.

Azure gelden beperkingen met betrekking tot het aantal gegevensschijven Hallo en de hoeveelheid bandbreedte die beschikbaar zijn, afhankelijk van de VM-grootte Hallo. Zie voor meer informatie [grootten voor virtuele machines](sizes.md).

Als u van schijf-striping voor Azure gegevensschijven gebruikmaakt, kunt u de Hallo richtlijnen te volgen:

* Maximum aantal gegevensschijven Hallo toegestaan voor VM-grootte Hallo koppelen.
* Opslagruimten gebruiken.
* Vermijd het gebruik van Azure-gegevensschijf cacheopties (cachebeleid = None).

Zie voor meer informatie [opslagruimten - ontwerpen voor prestaties](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).

## <a name="multiple-storage-accounts"></a>Meerdere opslagaccounts
Deze sectie geldt niet te[Azure beheerd schijven](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), omdat u geen afzonderlijke storage-accounts maken. 

Bij het ontwerpen van uw Azure Storage-omgeving voor niet-beheerde schijven kunt u meerdere opslagaccounts zoals Hallo aantal virtuele machines die u implementeert toeneemt. Deze aanpak kunt distribueren uit Hallo i/o over Hallo onderliggende Azure Storage-infrastructuur toomaintain optimale prestaties voor uw virtuele machines en toepassingen. Overweeg bij het ontwerpen van Hallo-toepassingen die u implementeert Hallo i/o-vereisten voor die elke virtuele machine heeft en het saldo van deze VMs over Azure Storage-accounts. Probeer tooavoid alle Hallo hoge i/o veeleisende van virtuele machines in de storage-accounts toojust Eén of twee groeperen.

Zie voor meer informatie over Hallo i/o-mogelijkheden van Hallo verschillende Azure Storage-opties en sommige maximumwaarden aanbevelen, [Azure storage schaalbaarheids- en prestatiedoelen](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

