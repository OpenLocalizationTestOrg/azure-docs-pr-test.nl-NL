---
title: Azure Redis-Cache Premium-laag van aaaIntroduction toohello | Microsoft Docs
description: Meer informatie over hoe toocreate Redis-persistentie, Redis clustering en VNET-ondersteuning voor uw Azure Redis-Cache-exemplaren van Premium-laag en beheren
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Inleiding toohello Azure Redis-Cache Premium-laag
Azure Redis-Cache is een gedistribueerd, beheerde cache waarmee u uiterst schaalbare en responsief toepassingen bouwen door zeer snelle toegang tooyour gegevens te verstrekken. 

Hallo die nieuwe Premium-laag is een Enterprise gereed laag, dat bestaat uit alle functies van de Hallo Standard-laag en meer, zoals betere prestaties, grotere werkbelastingen, herstel na noodgevallen, importeren/exporteren en betere beveiliging. Blijven lezen toolearn meer over de aanvullende functies Hallo van Hallo Premium cache-laag.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Betere prestaties ten opzichte van tooStandard of Basic laag
**Betere prestaties via standaard of Basic laag.** Caches in Hallo Premium-laag worden geïmplementeerd op hardware die snellere processors en biedt betere prestaties in vergelijking toohello Basic of Standard-laag. Premium-laag Caches hebben hogere doorvoer en lagere latenties. 

**Doorvoer voor Hallo dezelfde grootte Cache is hoger in Premium als vergeleken tooStandard laag.** Bijvoorbeeld, Hallo doorvoer van een 53 GB P4 (Premium)-cache is 250K aanvragen per seconde als vergeleken too150K voor C6 (standaard).

Zie voor meer informatie over de grootte, doorvoer en bandbreedte van premiumcaches [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Redis-gegevenspersistentie
Premium-laag Hallo kunt u toopersist Hallo cache-gegevens in een Azure Storage-account. In een Basic/standaard alle Hallo gegevens alleen in het geheugen worden opgeslagen in de cache. In geval van een onderliggende infrastructuur kunnen er problemen zijn mogelijk gegevensverlies. U wordt aangeraden gebruik Hallo Redis gegevens persistentie functie in Hallo Premium-laag tooincrease tolerantie tegen gegevensverlies. Azure Redis-Cache biedt RDB en AOF (binnenkort) opties in [Redis-persistentie](http://redis.io/topics/persistence). 

Zie voor instructies over het configureren van persistentie [hoe tooconfigure persistentie voor een Premium Azure Redis-Cache](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Redis-cluster
Als u wilt dat toocreate caches groter zijn dan 53 GB of tooshard gegevens over meerdere Redis-knooppunten wilt, kunt u Redis clustering die beschikbaar is in Hallo Premium-laag. Elk knooppunt bestaat uit een combinatie van primair/replica cache beheerd door Azure voor hoge beschikbaarheid. 

**Redis clustering biedt u maximale schaal en de doorvoer.** Doorvoer duurt lineair omdat u het aantal shards (knooppunten) in de cluster Hallo Hallo verhogen. Bv. Als u een cluster P4 van 10 shards maakt, is beschikbaar doorvoer Hallo 250K * 10 = 2,5 miljoen aanvragen per seconde. Zie Hallo [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) voor meer informatie over de grootte, doorvoer en bandbreedte van premiumcaches.

tooget gestart met clustering, Zie [hoe tooconfigure clustering voor een Premium Azure Redis-Cache](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Verbeterde veiligheid en isolatie
Caches gemaakt in de laag Basic- of Standard Hallo toegankelijk zijn op Hallo van openbare internet. Toegang tot de Cache beperkt op basis van de toegangssleutel Hallo is toohello. Met de Hallo Premium-laag kunt u verder ervoor zorgen dat alleen clients binnen een opgegeven netwerk toegang heeft tot Hallo Cache. U kunt implementeren Redis-Cache in een [Azure Virtual Network (VNet)](https://azure.microsoft.com/services/virtual-network/). U kunt alle Hallo functies van VNet, zoals subnetten, toegangscontrolebeleid en andere functies toofurther tooRedis toegang beperken.

Zie voor meer informatie [hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>Import/Export
Import/Export is een Azure Redis-Cache data management bewerking waarmee u tooimport gegevens in Azure Redis-Cache of het exporteren van gegevens van Azure Redis-Cache door te importeren en exporteren van een momentopname van een Redis-Cache Database (RDB) van een premium cache tooa pagina-blob in een Azure Storage-Account. Dit kunt u toomigrate tussen verschillende exemplaren van Azure Redis-Cache of vullen Hallo cache met gegevens voor het gebruik.

Importeren kan gebruikte toobring Redis compatibel RDB bestanden vanaf een willekeurige Redis-server uitgevoerd in een cloud of de omgeving, inclusief Redis uitgevoerd op Linux, Windows of elke cloudprovider zoals Amazon Web Services en andere zijn. Het importeren van gegevens is een eenvoudige manier toocreate een cache met vooraf ingestelde gegevens. Tijdens het importproces Hallo, Azure Redis-Cache Hallo RDB bestanden uit Azure storage in het geheugen geladen en vervolgens ingevoegd Hallo sleutels in Hallo-cache.

Exporteren kunt u tooexport Hallo opgeslagen gegevens in Azure Redis-Cache tooRedis compatibel RDB bestanden. U kunt deze functie toomove op gegevens uit een Azure Redis-Cache-exemplaar tooanother of tooanother Redis-server gebruiken. Tijdens het exportproces hello, wordt een tijdelijk bestand op Hallo VM dat hosts Hallo server-exemplaar van Azure Redis-Cache en Hallo bestand geüploade toohello aangewezen storage-account is gemaakt. Wanneer de exportbewerking Hallo is voltooid met de status van slagen of mislukken, wordt Hallo tijdelijk bestand verwijderd.

Zie voor meer informatie [hoe tooimport gegevens in en gegevens exporteren uit Azure Redis-Cache](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Opnieuw opstarten
premium-laag Hallo kunt u tooreboot een of meer knooppunten van de cache op aanvraag. Hiermee kunt u tootest uw toepassing voor tolerantie in Hallo gebeurtenis van een fout. U kunt Hallo knooppunten na opnieuw opstarten.

* Hoofdknooppunt van de cache
* Slave knooppunt van de cache
* Hoofd- en slave knooppunten van de cache
* Als u een premium-cache met clustering, kunt u opstarten Hallo master, slave of beide knooppunten voor afzonderlijke shards in Hallo-cache

Zie voor meer informatie [opnieuw opstarten](cache-administration.md#reboot) en [Veelgestelde vragen over het opnieuw opstarten](cache-administration.md#reboot-faq).

>[!NOTE]
>Opnieuw opstarten functionaliteit is nu ingeschakeld voor alle lagen van de Azure Redis-Cache.
>
>

## <a name="schedule-updates"></a>Updates plannen
Hallo geplande updatefunctie kunt u een onderhoudsvenster voor uw cache toodesignate. Wanneer het onderhoudsvenster hello wordt opgegeven, wordt een Redis-server bijgewerkt tijdens dit venster. toodesignate een onderhoudsvenster, selecteert u Hallo gewenst dagen en geef Hallo onderhoud-venster Beginuur voor elke dag. Houd er rekening mee dat de duur van het onderhoudsvenster Hallo ingesteld op UTC is. 

Zie voor meer informatie [updates plannen](cache-administration.md#schedule-updates) en [updates plannen Veelgestelde vragen over](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Alleen Redis-server updates worden uitgevoerd tijdens het Hallo geplande onderhoudsvenster. Hallo onderhoudsvenster is niet van toepassing op tooAzure updates of updates toohello VM-besturingssysteem.
> 
> 

## <a name="geo-replication"></a>Geo-replicatie

**Geo-replicatie** biedt een mechanisme voor het koppelen van twee exemplaren van Premium-laag Azure Redis-Cache. Een cache is aangewezen als Hallo primaire gekoppelde cache en andere als secundaire gekoppelde cache Hallo Hallo. Hallo secundaire gekoppelde cache wordt alleen-lezen en gegevens die zijn geschreven toohello primaire-cache is gerepliceerd toohello secundaire gekoppelde cache. Deze functionaliteit kan gebruikte tooreplicate een cache in Azure-regio's zijn.

Zie voor meer informatie [hoe tooconfigure Geo-replicatie voor Azure Redis-Cache](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>tooscale toohello premium-laag
tooscale toohello premium-laag, kies een van de premium-categorieën Hallo gewoon in Hallo **wijziging prijscategorie** blade. U kunt ook uw cache toohello premium-laag met PowerShell en CLI schalen. Zie voor stapsgewijze instructies [hoe tooScale Azure Redis-Cache](cache-how-to-scale.md) en [hoe tooautomate een vergroten/verkleinen bewerking](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Volgende stappen
Een cache maken en nieuwe functies van premium-laag Hallo verkennen.

* [Hoe tooconfigure persistentie voor een Premium Azure Redis-Cache](cache-how-to-premium-persistence.md)
* [Hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache](cache-how-to-premium-vnet.md)
* [Hoe tooconfigure clustering voor een Premium Azure Redis-Cache](cache-how-to-premium-clustering.md)
* [Hoe tooimport gegevens in en gegevens exporteren uit Azure Redis-Cache](cache-how-to-import-export-data.md)
* [Hoe tooadminister Azure Redis-Cache](cache-administration.md)

