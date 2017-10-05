---
title: Opslagoplossingen mogelijk voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over de sleutel ontwerpen en implementeren van de richtlijnen voor het implementeren van opslagoplossingen voor in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3c368f07-189b-4520-bbe2-f4080253bbf2
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7c5089b9db945b0e0f4523e53bb44c178ffd0781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-linux-vms"></a>Azure-opslag-infrastructuur richtlijnen voor virtuele Linux-machines

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het inzicht opslagbehoeften en overwegingen voor het bereiken van de prestaties van de optimale virtuele machine (VM).

## <a name="implementation-guidelines-for-storage"></a>Implementatie van richtlijnen voor opslag
Beslissingen te nemen:

* Gaat u beheerde Azure-schijven of niet-beheerde schijven gebruiken?
* Wilt u de Standard of Premium-opslag gebruiken voor uw workload?
* Moet u een schijf striping schijven groter is dan 4TB maken?
* Moet u een schijf striping optimale i/o-prestaties voor uw workload bereiken?
* Welke set van storage-accounts moet u voor het hosten van uw IT-werkbelasting of infrastructuur?

Taken:

* Bekijk de i/o-vereisten van de toepassingen die u implementeert en plannen van het juiste aantal en type van de storage-accounts.
* De set met behulp van de naamconventie storage-accounts maken. U kunt de Azure CLI of de portal gebruiken.

## <a name="storage"></a>Storage
Azure Storage is een belangrijk onderdeel van het implementeren en beheren van virtuele machines (VM's) en toepassingen. Azure Storage biedt services voor het opslaan van gegevens uit een bestand, niet-gestructureerde gegevens en berichten, en het is ook deel uit van de virtuele machines ondersteunende infrastructuur.

[Azure-beheerde schijven](../../storage/storage-managed-disks-overview.md) opslag voor u achter de schermen worden verwerkt. Met niet-beheerde schijven maken u storage-accounts voor het opslaan van de schijven (VHD-bestanden) voor uw Azure VM's. Wanneer het omhoog schalen, moet u ervoor zorgen dat u extra opslagaccounts hebt gemaakt, zodat u niet langer zijn dan de maximale IOPS voor opslag met een van uw schijven. Met beheerde schijven afhandeling van opslag, u niet langer beperkt door de limieten van het opslagaccount (zoals 20.000 IOPS / -account). U moet ook niet langer aangepaste installatiekopieën (VHD-bestanden) kopiëren naar meerdere accounts voor opslag. U kunt ze beheren op een centrale locatie – één opslagaccount per Azure-regio- en honderden van virtuele machines in een abonnement maken. U wordt aangeraden dat u beheerd schijven gebruiken voor nieuwe implementaties.

Er zijn twee soorten storage-accounts beschikbaar ter ondersteuning van virtuele machines:

* Standard-opslag-accounts u toegang krijgt tot blob-opslag (gebruikt voor het opslaan van de virtuele machine van Azure-schijven), table storage, queue storage- en opslag van bestanden.
* [Premium-opslag](../../storage/storage-premium-storage.md) accounts bieden ondersteuning voor schijven voor hoge prestaties, lage latentie voor i/o-intensieve werkbelastingen, zoals MongoDB Shard-cluster. Premium-opslag ondersteunt momenteel alleen Azure VM-schijven.

Azure maakt virtuele machines met een besturingssysteemschijf, een tijdelijke schijf en nul of meer optionele gegevensschijven. De besturingssysteemschijf en gegevensschijven zijn Azure-pagina-blobs, terwijl de tijdelijke schijf lokaal wordt opgeslagen op het knooppunt waar de machine woont. Wees voorzichtig bij het ontwerpen van toepassingen op deze tijdelijke schijf alleen gebruiken voor niet-permanente gegevens als de virtuele machine tussen hosts tijdens onderhoud kan worden gemigreerd. Gegevens die zijn opgeslagen op de tijdelijke schijf zou verloren zijn.

Duurzaamheid en maximale beschikbaarheid wordt verstrekt door de onderliggende opslag van de Azure-omgeving om ervoor te zorgen dat uw gegevens beveiligen tegen niet-gepland onderhoud of hardwarestoringen blijft. Als u uw Azure Storage-omgeving ontwerpt, kunt u kiezen voor replicatie van VM-opslag:

* lokaal binnen een bepaald Azure-datacenter
* over Azure-datacenters binnen een bepaald gebied
* over Azure-datacenters over verschillende regio's.

U kunt lezen [meer over de replicatieopties voor hoge beschikbaarheid](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Besturingssysteem-schijven en gegevensschijven hebben een maximale grootte van 4TB. Logische Volume Manager (LVM) kunt u deze limiet groter zijn dan door het groeperen van gegevensschijven ter beschikking logische volumes die groter zijn dan 1023GB met uw virtuele machine.

Er zijn bepaalde limieten voor schaalbaarheid bij het ontwerpen van uw implementaties van Azure Storage - voor meer informatie, Zie [Microsoft Azure-abonnement en service-limieten, quota's en beperkingen](../../azure-subscription-service-limits.md#storage-limits). Zie ook [Azure storage schaalbaarheids- en prestatiedoelen](../../storage/storage-scalability-targets.md).

Voor de toepassingsopslag van, kunt u opslaan ongestructureerde objectgegevens, zoals documenten, afbeeldingen, back-ups, configuratiegegevens, Logboeken, enzovoort. met behulp van blob-opslag. In plaats van uw toepassing schrijven naar een virtuele schijf die is gekoppeld aan de virtuele machine, kan de toepassing rechtstreeks naar Azure blob-opslag schrijven. BLOB-opslag biedt ook de mogelijkheid van [hot en cool opslaglagen](../../storage/storage-blob-storage-tiers.md) afhankelijk van uw behoeften van de beschikbaarheid en kostenbeperkingen.

## <a name="striped-disks"></a>Striped schijven
Naast het zodat u kunt schijven groter zijn dan 1023 GB te maken in veel gevallen verbetert met striping voor gegevensschijven de prestaties doordat meerdere blobs back-de opslag voor één volume. Met striping verloopt de i/o die vereist zijn om te schrijven en te lezen van gegevens uit één logische schijf parallel.

Azure gelden beperkingen met betrekking tot het aantal gegevensschijven en de hoeveelheid bandbreedte die beschikbaar zijn, afhankelijk van de VM-grootte. Zie voor meer informatie [grootten voor virtuele machines](sizes.md)

Als u van schijf-striping voor Azure gegevensschijven gebruikmaakt, kunt u de volgende richtlijnen:

* Koppel de maximum aantal gegevensschijven dat is toegestaan voor de VM-grootte.
* Gebruik LVM.
* Vermijd het gebruik van Azure-gegevensschijf cacheopties (cachebeleid = None).

Zie voor meer informatie [LVM configureren op een Linux-VM](configure-lvm.md).

## <a name="multiple-storage-accounts"></a>Meerdere opslagaccounts
Deze sectie niet van toepassing op [Azure beheerd schijven](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), omdat u geen afzonderlijke storage-accounts maken. 

Bij het ontwerpen van uw Azure Storage-omgeving voor niet-beheerde schijven kunt u meerdere opslagaccounts zoals het aantal virtuele machines die u implementeert toeneemt. Deze aanpak kunt verdelen van de i/o over de onderliggende Azure Storage-infrastructuur voor het onderhouden van optimale prestaties voor uw virtuele machines en toepassingen. Overweeg bij het ontwerpen van de toepassingen die u implementeert de i/o-vereisten voor die elke virtuele machine heeft en het saldo van deze VMs over Azure Storage-accounts. Probeer om te voorkomen dat de hoge I/O veeleisende VM's in op slechts één of twee opslagaccounts te groeperen.

Zie voor meer informatie over de i/o-functionaliteit van de verschillende opties voor Azure Storage en sommige maximumwaarden aanbevolen [Azure storage schaalbaarheids- en prestatiedoelen](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

