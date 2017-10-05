---
title: Azure Storage Scalability and Performance Targets | Microsoft Docs
description: Meer informatie over de schaalbaarheids- en prestatiedoelen voor Azure Storage, met inbegrip van capaciteit en snelheid van aanvragen voor binnenkomende en uitgaande bandbreedte voor beide standard en premium storage-accounts. Begrijpen prestatiedoelen voor partities in elk van de Azure Storage-services.
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 47a1d2b87269d40716b3dae02276207060b41c24
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Schaalbaarheids- en prestatiedoelen van Azure Storage
## <a name="overview"></a>Overzicht
Dit onderwerp beschrijft de schaalbaarheid en prestaties onderwerpen voor Microsoft Azure Storage. Zie voor een overzicht van andere Azure limieten [Azure-abonnement en Service-limieten, quota's en beperkingen](../../azure-subscription-service-limits.md).

> [!NOTE]
> Alle opslagaccounts worden uitgevoerd op de nieuwe platte netwerktopologie en ondersteunen de schaalbaarheids- en prestatiedoelen onderstaande, ongeacht wanneer ze zijn gemaakt. Zie voor meer informatie over de Azure Storage platte netwerkarchitectuur en schaalbaarheid [Microsoft Azure Storage: een maximaal beschikbare Cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> De schaalbaarheids- en prestatiedoelen hier vermeld zijn geavanceerde doelen, maar worden uitgevoerd. In alle gevallen, de frequentie van aanvragen en bandbreedte door uw opslag account is afhankelijk van de grootte van de objecten die zijn opgeslagen, de toegangspatronen gebruikt, en het type werkbelasting van uw toepassing uitvoert. Zorg ervoor dat voor het testen van uw service om te bepalen of de prestaties aan uw vereisten voldoet. Indien mogelijk plotselinge pieken in de frequentie van verkeer te voorkomen en ervoor te zorgen dat verkeer goed gedistribueerde meerdere partities.
> 
> Wanneer uw toepassing de limiet bereikt van wat een partitie voor de werkbelasting kan verwerken, gaat Azure Storage-foutcode 503 (Server bezet) of foutcode 500 (time-out voor de bewerking) antwoorden retourneren. Wanneer dit het geval is, moet de toepassing een exponentieel uitstel-beleid gebruiken voor nieuwe pogingen. De exponentieel uitstel kan de belasting op de partitie te verkleinen en te vereenvoudigen uit pieken in het verkeer voor deze partitie.
> 
> 

Als de behoeften van uw toepassing de schaalbaarheidsdoelen van een enkele storage-account overschrijdt, kunt u uw toepassing te gebruiken van meerdere storage-accounts maken en uw gegevensobjecten partitie tussen deze opslagaccounts. Zie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/) voor meer informatie over Volumeprijzen.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Schaalbaarheidsdoelen voor blobs, wachtrijen, tabellen en bestanden
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Schaalbaarheidsdoelen voor virtuele machine-schijven
[!INCLUDE [azure-storage-limits-vm-disks](../../../includes/azure-storage-limits-vm-disks.md)]

Zie [Windows VM-grootten](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [Linux VM-grootten](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.

## <a name="managed-virtual-machine-disks"></a>Beheerde virtuele-machineschijven

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Niet-beheerde virtuele-machineschijven
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Schaalbaarheidsdoelen voor Azure resourcemanager
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Partities in Azure-opslag
Elk object dat bevat gegevens die zijn opgeslagen in Azure Storage (BLOB's, berichten, entiteiten en bestanden) behoort tot een partitie en wordt geïdentificeerd door een partitiesleutel. De partitie bepaalt hoe Azure Storage load compromis tussen de BLOB's, berichten, entiteiten en bestanden op servers om te voldoen aan de behoeften van verkeer van die objecten. De partitiesleutel is uniek en wordt gebruikt om te zoeken naar een blob, het bericht of de entiteit.

Bovenstaande tabel [Schaalbaarheidsdoelen voor Standard-Opslagaccounts](#standard-storage-accounts) geeft een lijst van de prestatiedoelen voor één partitie voor elke service.

Partities invloed hebben op taakverdeling en schaalbaarheid voor elk van de storage-services in de volgende manieren:

* **BLOBs**: de partitiesleutel voor een blob is accountnaam + containernaam + blob-naam. Dit betekent dat elke blob een eigen partitie hebben kan als de belasting van de blob is vereist. BLOBs kunnen op veel servers worden gedistribueerd om de toegang tot uitbreiden, maar één blob kan alleen worden geleverd door één server. Blobs kunnen logisch worden gegroepeerd in blob-containers, maar er zijn geen partitionering gevolgen van deze groepering.
* **Bestanden**: de partitiesleutel voor een bestand is de sharenaam van naam + bestand-account. Dit betekent dat alle bestanden in een bestandsshare bevinden zich ook in één partitie.
* **Berichten**: de partitiesleutel voor een bericht is de accountnaam + wachtrijnaam, dus alle berichten in een wachtrij zijn ondergebracht in één partitie en door één server worden behandeld. Verschillende wachtrijen kunnen worden verwerkt door andere servers voor de taakverdeling voor echter veel wachtrijen een opslagaccount kan hebben.
* **Entiteiten**: de partitiesleutel voor een entiteit is het account naam + tabelnaam + partitie-sleutel, waarbij de partitiesleutel de waarde van de vereiste gebruiker gedefinieerde is **PartitionKey** eigenschap voor de entiteit. Alle entiteiten met dezelfde partitie sleutelwaarde in dezelfde partitie worden gegroepeerd en door de server met dezelfde partitie worden behandeld. Dit is een belangrijk punt om te begrijpen bij het ontwerpen van uw toepassing. De voordelen van de schaalbaarheid van entiteiten verspreid over meerdere partities met de voordelen van toegang voor het groeperen van entiteiten in één partitie moet worden verdeeld in uw toepassing.  

Een groot voordeel op een verzameling entiteiten in een tabel groeperen in één partitie is dat het is mogelijk atomic batchbewerkingen uitvoert via voor entiteiten in dezelfde partitie omdat een partitie op één server bestaat. Overweeg daarom als u uitvoeren van batchbewerkingen op een groep van entiteiten wilt, om ze te groeperen met dezelfde partitiesleutel. 

Aan de andere kant entiteiten die zich in dezelfde tabel, maar de verschillende partitiesleutels kan worden met gelijke taakverdeling over verschillende servers, waardoor het mogelijk om grotere schaalbaarheid.

Aanbevelingen voor het ontwerpen van partitioneren strategie voor tabellen vindt u gedetailleerde [hier](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Zie ook
* [Opslag prijsgegevens](https://azure.microsoft.com/pricing/details/storage/)
* [Azure-abonnement en Servicelimieten, quota's en beperkingen](../../azure-subscription-service-limits.md)
* [Premium Storage: opslag met hoge prestaties voor de werkbelasting van virtuele Azure-machines](../storage-premium-storage.md)
* [Azure Storage-replicatie](../storage-redundancy.md)
* [Microsoft Azure Storage prestaties en schaalbaarheid controlelijst](../storage-performance-checklist.md)
* [Microsoft Azure Storage: Een maximaal beschikbare Cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

