---
title: "Zakelijke continuïteit en herstel na noodgevallen (BCDR): Azure-gebieden gekoppeld | Microsoft Docs"
description: Meer informatie over Azure regionale koppelen, tooensure dat toepassingen robuuste tijdens data center-fouten zijn.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>Zakelijke continuïteit en herstel na noodgevallen (BCDR): Azure-gebieden gekoppeld

## <a name="what-are-paired-regions"></a>Wat zijn gekoppeld regio's?

Azure werkt op meerdere locaties Hallo wereld. Een Azure Geografie is een bepaald gebied van Hallo wereld met ten minste één Azure-regio. Een Azure-regio is een gebied binnen een Geografie, met een of meer datacenters.

Elke Azure-regio is gekoppeld aan een andere regio binnen Hallo hetzelfde Geografie, een combinatie van regionale samen te maken. Hallo-uitzondering is Brazilië-Zuid is gekoppeld aan buiten de geografische regio.

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

Afbeelding 1: Azure regionale paar diagram

| Geografie | Gekoppelde regio 's |  |
|:--- |:--- |:--- |
| Azië |Oost-Azië |Zuidoost-Azië |
| Australië |Australië - oost |Australië - zuidoost |
| Canada |Canada - centraal |Canada - oost |
| China |China - noord |China - oost|
| India |Centraal-India |Zuid-India |
| Japan |Japan - oost |Japan - west |
| Korea |Korea - centraal |Korea - zuid |
| Noord-Amerika |Noord-centraal VS |Zuid-centraal VS |
| Noord-Amerika |VS - oost |VS - west |
| Noord-Amerika |VS - oost 2 |VS - midden |
| Noord-Amerika |VS - west 2 |West-centraal VS |
| Europa |Noord-Europa |West-Europa |
| Japan |Japan - oost |Japan - west |
| Brazilië |Brazilië-Zuid (1) |Zuid-centraal VS |
| Amerikaanse overheid |VS (overheid) - Iowa |VS (overheid) - Virginia |
| Amerikaanse overheid |VS (overheid) - Virginia |VS (overheid) - Texas |
| Amerikaanse overheid |VS (overheid) - Texas |VS (overheid) - Arizona |
| Amerikaanse overheid |VS (overheid) - Arizona |VS (overheid) - Texas |
| VERENIGD KONINKRIJK |Verenigd Koninkrijk West |Verenigd Koninkrijk Zuid |
| Duitsland |Duitsland - centraal |Duitsland - noordoost |

Tabel 1 - toewijzing van Azure regionale paren

> (1) Brazilië-Zuid is uniek omdat deze is gekoppeld aan een regio buiten de eigen Geografie. Brazilië-Zuid secundaire regio is Zuid-centraal VS, maar er is geen Zuid-centraal VS van secundaire regio Brazilië-Zuid.


Het is raadzaam dat u workloads over regionale paren toobenefit uit Azure isolatie en beschikbaarheid repliceren. Bijvoorbeeld, geplande Azure systeemupdates sequentieel worden geïmplementeerd (niet op Hallo hetzelfde moment) tussen de gekoppelde regio's. Dat betekent dat zelfs in Hallo zeldzame geval van een defecte update, beide regio's worden niet beïnvloed tegelijkertijd. Bovendien in Hallo onwaarschijnlijke geval van een brede onderbreking, krijgt herstel van ten minste één regio buiten elk paar voorrang.

## <a name="an-example-of-paired-regions"></a>Een voorbeeld van een gekoppelde regio 's
Afbeelding 2 toont een hypothetische toepassing hello regionale paar gebruikt voor herstel na noodgevallen. Hallo groen cijfers Markeer Hallo regio-overschrijdende activiteiten drie Azure-Services (Azure compute, storage, en database) en hoe ze worden tooreplicate geconfigureerd tussen regio's. Hallo unieke voordelen van de implementatie in gekoppelde regio's worden gemarkeerd met Hallo oranje cijfers.

![Overzicht van de voordelen van de gekoppelde regio](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

Afbeelding 2: hypothetische Azure regionale paar

## <a name="cross-region-activities"></a>Regio-overschrijdende activiteiten
Afbeelding 2 als tooin waarnaar wordt verwezen.

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **Azure Compute (PaaS)** – moet u extra Reken-resources inrichten van tevoren tooensure bronnen beschikbaar zijn in een andere regio tijdens een noodgeval. Zie voor meer informatie [technische richtlijnen voor Azure tolerantie](resiliency/resiliency-technical-guidance.md).

![Opslag](./media/best-practices-availability-paired-regions/2Green.png) **Azure Storage** -geografisch redundante opslag (GRS) is standaard geconfigureerd als een Azure Storage-account is gemaakt. Met GRS wordt uw gegevens automatisch driemaal gerepliceerd Hallo primaire regio en driemaal in Hallo gekoppelde regio. Zie voor meer informatie [Azure redundantie opslagopties](storage/common/storage-redundancy.md).

![Azure SQL](./media/best-practices-availability-paired-regions/3Green.png) **Azure SQL-Databases** – met Azure SQL standaard Geo-replicatie, kunt u asynchrone replicatie van transacties tooa gekoppelde regio. Met premium geo-replicatie, kunt u replicatie tooany regio configureren in Hallo wereld; we raden echter implementeren van deze bronnen in een gekoppelde regio voor de meeste herstel na noodgevallen. Zie voor meer informatie [Geo-replicatie in Azure SQL Database](sql-database/sql-database-geo-replication-overview.md).

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png) **Azure Resource Manager** -Resource Manager biedt inherent logische isolatie van onderdelen van service management tussen regio's. Dit betekent dat logische storingen in één regio zijn minder waarschijnlijk tooimpact een andere.

## <a name="benefits-of-paired-regions"></a>Voordelen van het gekoppelde regio 's
Afbeelding 2 als tooin waarnaar wordt verwezen.  

![Isolatie](./media/best-practices-availability-paired-regions/5Orange.png)
**fysieke isolatie** – wanneer mogelijk uit Azure geeft de voorkeur aan ten minste 300 mijl van de scheiding tussen datacentra in de combinatie van een regionale, hoewel dit praktisch of mogelijk niet in alle regio's. Fysieke datacenter scheiding vermindert Hallo kans natuurramp, civiele unrest, stroomstoringen of fysieke netwerkstoringen tegelijk die invloed hebben op beide regio's. Isolatie is onderwerp toohello beperkingen binnen Hallo Geografie (Geografie grootte, power/netwerkbeschikbaarheid infrastructuur, voorschriften, enzovoort).  

![Replicatie](./media/best-practices-availability-paired-regions/6Orange.png)
**Platform geleverde replicatie** -sommige services zoals geografisch redundante opslag bieden automatische replicatie toohello gekoppelde regio.

![Herstel](./media/best-practices-availability-paired-regions/7Orange.png)
**regio herstel volgorde** – In geval van een brede onderbreking Hallo herstel van één regio buiten elk paar wordt geplaatst. Toepassingen die zijn geïmplementeerd op gekoppelde regio's zijn gegarandeerd toohave een Hallo regio's met prioriteit is hersteld. Als een toepassing wordt geïmplementeerd in regio's die niet zijn gekoppeld, herstel mogelijk een vertraging – in Hallo slechtste case Hallo gekozen regio's kunnen de Hallo laatste twee toobe hersteld.

![Updates](./media/best-practices-availability-paired-regions/8Orange.png)
**opeenvolgende updates** – systeemupdates Azure gepland zijn uitgerold toopaired regio's worden na elkaar (niet op Hallo hetzelfde moment) toominimize uitvaltijd, Hallo effect van bugs en logische fouten in het zeldzame geval Hallo van een ongeldige update.

![Gegevens](./media/best-practices-availability-paired-regions/9Orange.png)
**gegevens hand vestigingsplaats** – een regio deel uitmaakt van Hallo dezelfde Geografie als de paar (met uitzondering van Hallo van Brazilië-Zuid) in de volgorde toomeet hand vestigingsplaats eisen voor btw en het recht afdwinging bevoegdheid doeleinden.
