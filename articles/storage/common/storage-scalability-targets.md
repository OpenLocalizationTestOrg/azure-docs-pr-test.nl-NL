---
title: aaaAzure Storage Scalability and Performance Targets | Microsoft Docs
description: Meer informatie over de schaalbaarheids- en prestatiedoelen Hallo voor Azure Storage, met inbegrip van capaciteit en snelheid van aanvragen voor binnenkomende en uitgaande bandbreedte voor beide standard en premium storage-accounts. Begrijpen prestatiedoelen voor partities binnen elke hello Azure Storage-services.
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
ms.openlocfilehash: 7afe4366a02887b4e3d9781c26c8adda81adce95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Schaalbaarheids- en prestatiedoelen van Azure Storage
## <a name="overview"></a>Overzicht
Dit onderwerp beschrijft de schaalbaarheid en prestaties onderwerpen Hallo voor Microsoft Azure Storage. Zie voor een overzicht van andere Azure limieten [Azure-abonnement en Service-limieten, quota's en beperkingen](../../azure-subscription-service-limits.md).

> [!NOTE]
> Alle opslagaccounts worden uitgevoerd op Hallo nieuwe platte-netwerktopologie en ondersteunen Hallo schaalbaarheids- en prestatiedoelen onderstaande, ongeacht wanneer ze zijn gemaakt. Zie voor meer informatie over hello Azure Storage platte netwerkarchitectuur en schaalbaarheid [Microsoft Azure Storage: een maximaal beschikbare Cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> Hallo schaalbaarheids- en prestatiedoelen hier vermeld zijn geavanceerde doelen, maar worden uitgevoerd. In alle gevallen Hallo aanvraag snelheid en bandbreedte bereikt door uw storage-account is afhankelijk van de grootte van de objecten die zijn opgeslagen, Hallo Hallo toegangspatronen gebruikt en Hallo type werkbelasting dat uw toepassing uitvoert. Worden tootest ervoor dat uw service toodetermine of de prestaties aan uw vereisten voldoet. Indien mogelijk plotselinge pieken in de frequentie van verkeer Hallo voorkomen en ervoor te zorgen dat verkeer goed gedistribueerde meerdere partities.
> 
> Wanneer uw toepassing hello limiet van wat een partitie voor uw workload verwerken kan bereikt, Azure Storage tooreturn-foutcode 503 (Server bezet) wordt gestart of foutcode 500 (time-out voor de bewerking) antwoorden. Wanneer dit het geval is, moet Hallo toepassing een exponentieel uitstel-beleid gebruiken voor nieuwe pogingen. Hallo exponentieel uitstel kan Hallo belasting op Hallo partitie toodecrease en tooease uit pieken in verkeer toothat partitie.
> 
> 

Als Hallo van uw toepassing hello schaalbaarheidsdoelen van een enkele opslagaccount overschrijdt behoeften, kunt u meerdere opslagaccounts voor uw toepassing toouse bouwen en partitie uw gegevensobjecten over de storage-accounts. Zie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/) voor meer informatie over Volumeprijzen.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Schaalbaarheidsdoelen voor blobs, wachtrijen, tabellen en bestanden
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
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
Elk object dat bevat gegevens die zijn opgeslagen in Azure Storage (BLOB's, berichten, entiteiten en bestanden) behoort tooa partitie en wordt geïdentificeerd door een partitiesleutel. Hallo partitie bepaalt hoe Azure Storage load compromis tussen de BLOB's, berichten, entiteiten en bestanden tussen servers toomeet Hallo verkeer behoeften van die objecten. Hallo partitiesleutel is uniek en gebruikte toolocate is een blob, het bericht of de entiteit.

bovenstaande Hallo-tabel [Schaalbaarheidsdoelen voor Standard-Opslagaccounts](#standard-storage-accounts) lijsten Hallo prestatiedoelen voor één partitie voor elke service.

Partities invloed hebben op taakverdeling en schaalbaarheid voor elk van de opslagservices Hallo in de volgende manieren Hallo:

* **BLOBs**: Hallo partitiesleutel voor een blob is accountnaam + containernaam + blob-naam. Dit betekent dat elke blob een eigen partitie hebben kan als de belasting op Hallo blob is vereist. BLOBs kunnen worden gedistribueerd op veel servers in de volgorde tooscale uit toegang toothem, maar één blob kan alleen worden geleverd door één server. Blobs kunnen logisch worden gegroepeerd in blob-containers, maar er zijn geen partitionering gevolgen van deze groepering.
* **Bestanden**: Hallo partitiesleutel voor een bestand is de sharenaam van naam + bestand-account. Dit betekent dat alle bestanden in een bestandsshare bevinden zich ook in één partitie.
* **Berichten**: Hallo partitiesleutel voor een bericht is Hallo accountnaam + wachtrijnaam, zodat alle berichten in een wachtrij zijn ondergebracht in één partitie en door één server worden behandeld. Verschillende wachtrijen kunnen worden verwerkt door andere servers toobalance Hallo laden voor het echter veel wachtrijen een opslagaccount kan hebben.
* **Entiteiten**: Hallo partitiesleutel voor een entiteit is accountnaam + tabelnaam + partitiesleutel, waarbij Hallo partitiesleutel Hallo-waarde van Hallo vereist is gebruiker gedefinieerde **PartitionKey** eigenschap voor Hallo entiteit. Alle entiteiten met dezelfde waarde voor de partitiesleutel worden gegroepeerd op Hallo dezelfde partitie en worden geleverd door Hallo dezelfde Hallo partitie-server. Dit is een belangrijk punt toounderstand bij het ontwerpen van uw toepassing. Hallo schaalbaarheid voordelen van entiteiten verspreid over meerdere partities met Hallo gegevens toegang voordelen van het groeperen van entiteiten in één partitie moet worden verdeeld in uw toepassing.  

Een groot voordeel toogrouping een set van entiteiten in een tabel in een enkele partitie is dat het mogelijk tooperform-atomic batchbewerkingen is voor alle entiteiten in Hallo dezelfde partitie omdat een partitie op één server bestaat. Overweeg daarom als u tooperform batchbewerkingen op een groep van entiteiten wenst, om ze te groeperen met Hallo dezelfde partitiesleutel. 

Op Hallo daarentegen, entiteiten die zich in Hallo dezelfde tabel, maar verschillende partitiesleutels kunnen gelijkmatig verdeeld zijn over verschillende servers, waardoor het mogelijk toohave grotere schaalbaarheid.

Aanbevelingen voor het ontwerpen van partitioneren strategie voor tabellen vindt u gedetailleerde [hier](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Zie ook
* [Opslag prijsgegevens](https://azure.microsoft.com/pricing/details/storage/)
* [Azure-abonnement en Servicelimieten, quota's en beperkingen](../../azure-subscription-service-limits.md)
* [Premium Storage: opslag met hoge prestaties voor de werkbelasting van virtuele Azure-machines](../storage-premium-storage.md)
* [Azure Storage-replicatie](../storage-redundancy.md)
* [Microsoft Azure Storage prestaties en schaalbaarheid controlelijst](../storage-performance-checklist.md)
* [Microsoft Azure Storage: Een maximaal beschikbare Cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

