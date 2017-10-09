---
title: aaaWhat toodo in geval van een Azure Storage-storing Hallo | Microsoft Docs
description: Welke toodo in Hallo-gebeurtenis van een storing Azure Storage
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: 93e1e831c35b96b8bf190fa2b56ab89350bbac13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>Welke toodo als een Azure Storage-storing optreedt
Bij Microsoft werken we harde toomake ervoor dat onze services altijd beschikbaar zijn. Soms dwingt afgezien van onze invloed ons op een manier die niet-geplande storingen in een of meer regio's veroorzaken. toohelp verwerken van deze exemplaren zeldzame, bieden we Hallo op hoog niveau richtlijnen voor Azure Storage-services te volgen.

## <a name="how-tooprepare"></a>Hoe tooprepare
Het is essentieel voor elke klant tooprepare hun eigen noodherstelplan. Hallo inspanning toorecover van een storing opslag betekent meestal dat zowel operations personeel en geautomatiseerde procedures in de volgorde tooreactivate uw toepassingen in een werkende staat. Raadpleeg toohello Azure-documentatie hieronder toobuild uw eigen noodherstelplan:

* [Herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen](/azure/architecture/resiliency/disaster-recovery-high-availability-azure-applications.md)
* [Technische richtlijnen voor flexibiliteit van Azure](/azure/architecture/resiliency.md)
* [Azure Site Recovery-service](https://azure.microsoft.com/services/site-recovery/)
* [Azure Storage-replicatie](storage-redundancy.md)
* [Azure Backup-service](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>Hoe toodetect
Hallo aanbevolen manier toodetermine hello Azure servicestatus is toosubscribe toohello [Azure Service Health Dashboard](https://azure.microsoft.com/status/).

## <a name="what-toodo-if-a-storage-outage-occurs"></a>Welke toodo als er een storing opslag optreedt
Als een of meer opslagservices tijdelijk niet beschikbaar op een of meer regio's zijn, zijn er twee opties voor u tooconsider. Als u directe toegang tot tooyour gegevens willen, overweeg dan optie 2.

### <a name="option-1-wait-for-recovery"></a>Optie 1: Wacht voor herstel
In dit geval is geen actie ondernemen vereist. We werken naar eer en geweten toorestore hello Azure servicebeschikbaarheid. U kunt de servicestatus Hallo op Hallo bewaken [Azure Service Health Dashboard](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Optie 2: Gegevens kopiëren van secundaire
Als u hebt gekozen [geografisch redundante opslag met leestoegang (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (aanbevolen) voor uw storage-accounts, hebt u leestoegang tooyour gegevens van de secundaire regio Hallo. U kunt hulpprogramma's gebruiken zoals [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), en Hallo [bibliotheek voor gegevensverplaatsing van Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) toocopy gegevens van de secundaire regio Hallo in een ander opslagaccount in een unimpacted regio en vervolgens punt uw toepassingen toothat storage-account voor zowel lezen en schrijven van beschikbaarheid.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>Welke tooexpect als er een failover opslag optreedt
Als u hebt gekozen [geografisch redundante opslag (GRS)](storage-redundancy.md#geo-redundant-storage) of [geografisch redundante opslag met leestoegang (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (aanbevolen), Azure Storage houdt uw gegevens duurzaam in twee gebieden (primair en secundair). In beide regio's houdt de Azure Storage voortdurend meerdere replica's van uw gegevens.

Wanneer een regionale noodgeval is van invloed op uw primaire regio, proberen we eerst toorestore Hallo service in deze regio. Afhankelijk van Hallo aard van Hallo na noodgevallen en de effecten, in sommige soms wordt mogelijk niet kunnen toorestore Hallo primaire regio. Op dat moment wordt uitgevoerd, er een geo-failover. Hallo regio-overschrijdende gegevensreplicatie is een asynchroon proces waarbij een vertraging, zodat het mogelijk dat wijzigingen die nog niet zijn gerepliceerd toohello secundaire regio kan zijn mogelijk verloren gegaan. U kunt een query Hallo ['Tijd van laatste synchronisatie' van uw opslagaccount](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) tooget details op Hallo replicatiestatus.

Een aantal punten met betrekking tot Hallo geo failover opslagervaring:

* Opslag-geo-failover wordt alleen geactiveerd door hello Azure Storage team: Er is geen klant-actie vereist.
* Uw bestaande storage-service-eindpunten voor blobs, tabellen, wachtrijen en -bestanden blijven Hallo dezelfde na een failover Hallo; Hallo DNS-vermelding moet toobe bijgewerkt tooswitch van Hallo primaire regio toohello secundaire regio.
* Voor en tijdens het Hallo geo-failover, u hebt geen schrijftoegang tooyour opslagaccount vanwege toohello gevolgen van het Hallo-noodherstel, maar u kunt nog steeds lezen van de secundaire Hallo als uw storage-account is geconfigureerd als een RA-GRS.
* Lees- en schrijftoegang tooyour storage-account wordt hervat wanneer Hallo geo-failover is voltooid en DNS-wijzigingen die zijn doorgegeven hello, Dit verwijst toobe toowhat gebruikt uw secundaire eindpunt. 
* Houd er rekening mee dat u schrijftoegang hebt als u GRS of RA-GRS geconfigureerd voor het Hallo-opslagaccount. 
* U kunt een query ['Laatste Geo Failover keer' van uw opslagaccount](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget om meer details.
* Na een failover Hallo uw storage-account volledig functioneert, maar in een 'gedegradeerde' status, zoals deze wordt daadwerkelijk gehost in een zelfstandige regio met geen geo-replicatie mogelijk. toomitigate dit risico, we Hallo van de oorspronkelijke primaire regio en vervolgens een geo-failback wilt toorestore Hallo oorspronkelijke staat herstellen. Als de oorspronkelijke primaire regio Hallo is een onherstelbare, wordt er een andere secundaire regio toewijzen.
  Voor meer informatie over het Hallo-infrastructuur van Azure Storage geo-replicatie, raadpleegt u toohello artikel op Hallo Storage teamblog over [opties voor redundantie en RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Aanbevolen procedures voor het beveiligen van uw gegevens
Er zijn enkele aanbevolen methoden tooback van uw opslaggegevens regelmatig.

* VM-schijven gebruik Hallo [Azure Backup-service](https://azure.microsoft.com/services/backup/) tooback up Hallo VM-schijven die door uw virtuele Azure-machines gebruikt.
* Blok-blobs: Maak een [momentopname](https://msdn.microsoft.com/library/azure/hh488361.aspx) van elk blok-blob of Hallo blobs tooanother storage-account in met behulp van een andere regio kopiëren [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), of Hallo [ Azure bibliotheek voor gegevensverplaatsing](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Gebruik tabellen – [AzCopy](storage-use-azcopy.md) tooexport Hallo tabelgegevens in een ander opslagaccount in een andere regio.
* Bestanden – gebruiken [AzCopy](storage-use-azcopy.md) of [Azure PowerShell](storage-powershell-guide-full.md) toocopy uw tooanother File storage-account in een andere regio.

Voor informatie over het maken van toepassingen die volledig te van de functie Hallo RA-GRS profiteren check [ontwerpen van maximaal beschikbare toepassingen RA-GRS-opslag](../storage-designing-ha-apps-with-ragrs.md)

