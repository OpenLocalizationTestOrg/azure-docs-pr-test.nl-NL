---
title: aaaHow toomonitor Azure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe toomonitor Hallo status en prestaties van uw Azure Redis-Cache-exemplaren
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>Hoe toomonitor Azure Redis-Cache
Maakt gebruik van Azure Redis-Cache [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) tooprovide verschillende opties voor het bewaken van uw cache-exemplaren. U kunt metrische gegevens weergeven, metrische gegevens grafieken toohello Startboard vastmaken Hallo datum en tijd bereik van de bewaking van grafieken aanpassen, toevoegen en metrische gegevens verwijderen uit Hallo grafieken en waarschuwingen instellen wanneer aan bepaalde voorwaarden wordt voldaan. Deze hulpprogramma's inschakelen u toomonitor Hallo status van uw Azure Redis-Cache-exemplaren en uw cache in toepassingen te beheren.

Metrische gegevens voor Azure Redis-Cache-exemplaren worden verzameld met behulp van Hallo Redis [INFO](http://redis.io/commands/info) opdracht ongeveer twee keer per minuut en automatisch opgeslagen voor 30 dagen (Zie [cache metrische gegevens exporteren](#export-cache-metrics) tooconfigure een andere bewaarbeleid) zodat ze kunnen worden weergegeven in Hallo metrische gegevens grafieken en geëvalueerd door regels voor waarschuwingen. Zie voor meer informatie over Hallo verschillende INFO waarden gebruikt voor elke metriek cache [beschikbare metrische gegevens en de rapportage van intervallen](#available-metrics-and-reporting-intervals).

<a name="view-cache-metrics"></a>

maatstaven voor tooview cache [Bladeren](cache-configure.md#configure-redis-cache-settings) tooyour cache-exemplaar in Hallo [Azure-portal](https://portal.azure.com).  Azure Redis-Cache biedt een aantal ingebouwde grafieken op Hallo **overzicht** blade en Hallo **Redis metrische gegevens** blade. Elke grafiek kan worden aangepast door het toevoegen of verwijderen van metrische gegevens en Hallo reporting interval wijzigen.

![Metrische gegevens redis](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>Diagrammen van vooraf geconfigureerde metrische gegevens weergeven

Hallo **overzicht** blade Hallo volgen van vooraf geconfigureerde bewaking grafieken bevat.

* [Bewaking van grafieken](#monitoring-charts)
* [Gebruik grafieken](#usage-charts)

### <a name="monitoring-charts"></a>Bewaking van grafieken
Hallo **bewaking** sectie in Hallo **overzicht** blade bevat **treffers en Cachemissers**, **opgehaald en ingesteld**, **verbindingen**, en **totale opdrachten** grafieken.

![Bewaking van grafieken](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>Gebruik grafieken
Hallo **gebruik** sectie in Hallo **overzicht** blade bevat **serverbelasting Redis**, **geheugengebruik**, **netwerkbandbreedte** , en **CPU-gebruik** grafieken en worden ook weergegeven Hallo **prijscategorie** voor Hallo cache-exemplaar.

![Gebruik grafieken](./media/cache-how-to-monitor/redis-cache-usage-part.png)

Hallo **prijscategorie** geeft Hallo cache prijzen laag en te kunnen worden gebruikt[scale](cache-how-to-scale.md) Hallo cache tooa andere prijscategorie.

## <a name="view-metrics-with-azure-monitor"></a>Metrische gegevens weergeven met Azure-monitor
tooview Redis metrische gegevens en maken van aangepaste grafieken met behulp van Azure Monitor, klikt u op **metrische gegevens** van Hallo **Resource menu**, en aanpassen van de grafiek met Hallo gewenst metrische gegevens en de rapportage-grafiektype-interval en meer.

![Metrische gegevens redis](./media/cache-how-to-monitor/redis-cache-monitor.png)

Zie voor meer informatie over het werken met metrische gegevens met behulp van Azure Monitor [overzicht van metrische gegevens in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>Cache metrische gegevens exporteren
Cache metrische gegevens in de Azure-Monitor zijn standaard [30 dagen bewaard](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) en vervolgens verwijderd. toopersist uw cache metrische gegevens langer dan 30 dagen, kunt u [aanwijzen van een opslagaccount](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) en geef een **bewaartermijn (dagen)** beleid voor de metrische gegevens van uw cache. 

een opslagaccount voor de metrische gegevens van uw cache tooconfigure:

1. Klik op **Diagnostics** van Hallo **Resource menu** in Hallo **Redis-Cache** blade.
2. Klik op **op**.
3. Controleer **tooa opslagaccount archiveren**.
4. Selecteer Hallo storage-account in welke toostore Hallo cache metrische gegevens.
5. Controleer Hallo **1 minuut** selectievakje in en geef een **bewaartermijn (dagen)** beleid. Als u niet wilt dat tooapply bewaarbeleid en permanent bewaren van gegevens, stelt u **bewaartermijn (dagen)** te**0**.
6. Klik op **Opslaan**.

![Diagnostische gegevens redis](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>In aanvulling tooarchiving uw cache metrische gegevens toostorage, kunt u ook [stream ze tooan Event hub of verzend deze tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

tooaccess metrische gegevens over uw, kunt u deze bekijken in hello Azure portal, zoals eerder in dit artikel wordt beschreven en u kunt ze ook openen met behulp van Hallo [REST API voor de metrische gegevens van de Monitor van de Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

> [!NOTE]
> Als u opslagaccounts wijzigt, Hallo-gegevens in de opslagaccount Hallo eerder geconfigureerde blijft beschikbaar voor downloaden, maar deze niet wordt weergegeven in hello Azure-portal.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>Beschikbare metrische gegevens en de rapportage van intervallen
Cache metrische gegevens worden gerapporteerd met behulp van verschillende reporting intervallen, met inbegrip van **voorbij uur**, **vandaag**, **afgelopen week**, en **aangepaste**. Hallo **metriek** blade voor elke grafiek metrische gegevens Hallo gemiddelde, de minimale en maximale waarden voor elke metriek wordt in de grafiek Hallo en sommige metrische gegevens wordt een totaal voor Hallo reporting interval. 

Elke metriek bevat twee versies. Een metriek meet prestaties voor Hallo volledige cachegeheugen en caches die gebruikmaken van [clustering](cache-how-to-premium-clustering.md), een tweede versie van Hallo metriek met `(Shard 0-9)` in Hallo naam metingen prestaties voor een enkele shard in een cache. Bijvoorbeeld als een cache heeft 4 shards `Cache Hits` totale hoeveelheid treffers voor de hele cache Hallo Hallo en `Cache Hits (Shard 3)` is zojuist Hallo treffers voor die shard Hallo-cache.

> [!NOTE]
> Zelfs wanneer Hallo cache niet actief is zonder actieve client verbonden toepassingen, ziet u mogelijk een aantal cache-activiteit, zoals verbonden clients, geheugengebruik en bewerkingen die worden uitgevoerd. Deze activiteit is normaal tijdens Hallo van een Azure Redis-Cache-exemplaar.
> 
> 

| Gegevens | Beschrijving |
| --- | --- |
| Treffers in cache |Hallo aantal treffers sleutel tijdens Hallo opgegeven reporting interval. Dit wijst te`keyspace_hits` van Hallo Redis [INFO](http://redis.io/commands/info) opdracht. |
| Cachemissers |Hallo aantal mislukte sleutel zoekacties tijdens Hallo opgegeven reporting interval. Dit wijst te`keyspace_misses` van Hallo INFO Redis-opdracht. Cachemissers betekenen niet noodzakelijkerwijs dat er is een probleem met het Hallo-cache. Wanneer u de cache-aside ' programming patroon hello, een toepassing ziet er bijvoorbeeld eerste in de cache Hallo voor een item. Hello item is geen er (Cachemisser), Hallo item wordt opgehaald uit de database Hallo als toohello cache voor de volgende keer toegevoegd. Cachemissers zijn normaal gedrag voor cache-aside ' programming patroon Hallo. Als Hallo aantal Cachemissers groter is dan verwacht, controleert u toepassingslogica Hallo die gevuld en leest uit Hallo-cache. Als items zijn wordt verwijderd uit de cache Hallo vanwege toomemory druk vervolgens kan er een aantal missers in cache, maar een betere metrische toomonitor voor geheugendruk zou zijn `Used Memory` of `Evicted Keys`. |
| Verbonden Clients |Hallo aantal verbindingen toohello clientcache tijdens Hallo opgegeven reporting interval. Dit wijst te`connected_clients` van Hallo INFO Redis-opdracht. Eenmaal Hallo [verbindingslimiet](cache-configure.md#default-redis-server-configuration) latere verbindingspogingen toohello cache mislukt is bereikt. Denk eraan dat zelfs als er geen actieve clienttoepassing, zijn er mogelijk nog steeds zijn enkele exemplaren van de verbonden clients vanwege toointernal processen en verbindingen. |
| Verwijderde sleutels |Hallo aantal items verwijderd uit de cache Hallo tijdens Hallo opgegeven reporting interval vanwege toohello `maxmemory` limiet. Dit wijst te`evicted_keys` van Hallo INFO Redis-opdracht. |
| Verlopen sleutels |aantal items Hallo verlopen uit cache Hallo tijdens Hallo opgegeven reporting interval. Deze waarde toegewezen te`expired_keys` van Hallo INFO Redis-opdracht. |
| Totale aantal sleutels  | Hallo maximum aantal sleutels in de cache Hallo tijdens Hallo voorbij reporting periode. Dit wijst te`keyspace` van Hallo INFO Redis-opdracht. Totale aantal sleutels retourneert vanwege tooa beperking van metrische gegevens systeem, voor caches met clustering is ingeschakeld, onderliggende Hallo Hallo kunt u het maximum aantal sleutels van Hallo shard die Hallo kunt u het maximum aantal sleutels tijdens Hallo reporting interval had.  |
| Opgehaald |Hallo aantal get-bewerkingen uit cache Hallo tijdens Hallo opgegeven reporting interval. Deze waarde is de som van de volgende Hallo Hallo waarden van Hallo Redis INFO opdracht Alles: `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit`, en `cmdstat_getrange`, en is gelijkwaardig toohello totaal aantal treffers in cache en Missers tijdens Hallo reporting interval. |
| Redis belasting van de Server |Hallo percentage van de cycli welke Hallo Redis-server is bezig met de verwerking en niet wachten op niet-actieve voor berichten. Als deze teller 100 betekent Hallo Redis-server een maximum prestaties heeft bereikt en kan niet worden verwerkt door Hallo CPU moet u een sneller werken. Als u hoge belasting van Redis-Server ziet ziet u uitzonderingen voor time-outs in Hallo-client. In dit geval moet u omhoog schalen of uw gegevens in meerdere caches partitioneren. |
| Sets |het aantal set operations toohello-cache tijdens Hallo Hallo opgegeven reporting interval. Deze waarde is de som van de volgende Hallo Hallo waarden van Hallo Redis INFO opdracht Alles: `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` , en `cmdstat_setnx`. |
| Totaal aantal bewerkingen |Totaal aantal opdrachten verwerkt door de server van de cache Hallo tijdens Hallo Hallo opgegeven reporting interval. Deze waarde toegewezen te`total_commands_processed` van Hallo INFO Redis-opdracht. Houd er rekening mee dat wanneer Azure Redis-Cache wordt gebruikt voor pub subitems er worden geen metrische gegevens voor `Cache Hits`, `Cache Misses`, `Gets`, of `Sets`, maar er zijn `Total Operations` metrische gegevens die overeenkomen met Hallo cache gebruik voor pub subitems bewerkingen. |
| Gebruikt geheugen |Hallo hoeveelheid cachegeheugen gebruikt voor de sleutel/waarde-paren in de cache in MB Hallo tijdens Hallo opgegeven reporting interval. Deze waarde toegewezen te`used_memory` van Hallo INFO Redis-opdracht. Dit omvat geen metagegevens of fragmentatie. |
| Gebruikt geheugen RSS |Hallo hoeveelheid cache-geheugen in MB tijdens Hallo opgegeven reporting interval gebruikt, met inbegrip van fragmentatie en metagegevens. Deze waarde toegewezen te`used_memory_rss` van Hallo INFO Redis-opdracht. |
| CPU |Hallo CPU-gebruik van hello Azure Redis-Cache-server als een percentage tijdens Hallo opgegeven reporting interval. Deze waarde toegewezen toohello besturingssysteem `\Processor(_Total)\% Processor Time` prestatiemeteritem. |
| Cache lezen |Hallo en de hoeveelheid gegevens gelezen uit de cache Hallo in Megabytes per seconde (MB/s) tijdens Hallo opgegeven reporting interval. Deze waarde is afgeleid van Hallo netwerkinterfacekaarten die ondersteuning bieden voor Hallo virtuele machine die als host fungeert voor Hallo-cache en is niet Redis specifieke. **Deze waarde komt overeen toohello netwerkbandbreedte gebruikt door deze cache. Als u tooset van waarschuwingen voor bandbreedtelimieten van server side netwerk wilt, moet u deze maken gebruik van deze `Cache Read` teller. Zie [deze tabel](cache-faq.md#cache-performance) voor Hallo in acht genomen ondergrenzen voor verschillende cache prijzen lagen en grootten voor de bandbreedte.** |
| Cache schrijven |Hallo hoeveelheid gegevens toohello cache in MB per seconde (MB/s) tijdens de opgegeven reporting interval Hallo geschreven. Deze waarde is afgeleid van Hallo netwerkinterfacekaarten die ondersteuning bieden voor Hallo virtuele machine die als host fungeert voor Hallo-cache en is niet Redis specifieke. Deze waarde komt overeen toohello netwerkbandbreedte van gegevens die toohello cache van Hallo-client wordt verzonden. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Waarschuwingen
U kunt tooreceive waarschuwingen op basis van de logboeken van metrische gegevens en activiteit kunt configureren. Azure Monitor kunt u een waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd tooconfigure:

* E-mailmelding verzenden
* een webhook aanroepen
* Een Azure Logic App aanroepen

waarschuwingsregels voor uw cache tooconfigure klikt u op **waarschuwing regels** van Hallo **Resource menu**.

![Bewaking](./media/cache-how-to-monitor/redis-cache-monitoring.png)

Zie voor meer informatie over het configureren en het gebruik van waarschuwingen [overzicht van waarschuwingen](../monitoring-and-diagnostics/insights-alerts-portal.md).

## <a name="activity-logs"></a>Activiteitenlogboeken
Activiteitenlogboeken bieden inzicht in Hallo-bewerkingen die zijn uitgevoerd op uw Azure Redis-Cache-exemplaren. Het was voorheen bekend als 'controlelogboeken' of 'operationele logs'. Met activiteitenlogboeken, kunt u Hallo bepalen ' wat, wie, en wanneer ' voor een (PUT, POST, verwijderen schrijfbewerkingen) die zijn gemaakt op uw Azure Redis-Cache-exemplaren. 

> [!NOTE]
> Activiteitenlogboeken bevatten geen leesbewerkingen (GET).
>
>

tooview activiteitenlogboeken voor uw cache, klikt u op **activiteitenlogboeken** van Hallo **Resource menu**.

Zie voor meer informatie over activiteitenlogboeken [overzicht van hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).











