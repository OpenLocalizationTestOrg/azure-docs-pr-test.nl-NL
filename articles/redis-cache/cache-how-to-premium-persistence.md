---
title: aaaHow tooconfigure gegevenspersistentie voor een Premium Azure Redis-Cache
description: Meer informatie over hoe tooconfigure en uw Azure Redis-Cache-exemplaren van Premium-laag voor gegevenspersistentie beheren
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>Hoe tooconfigure gegevenspersistentie voor een Premium Azure Redis-Cache
Azure Redis-Cache heeft verschillende cache aanbiedingen die flexibiliteit bij het Hallo-keuze van de cachegrootte en -onderdelen bieden, met inbegrip van Premium-laag functies zoals clustering, persistentie en virtual network-ondersteuning. Dit artikel wordt beschreven hoe tooconfigure persistentie in een premium Azure Redis-Cache exemplaar.

Zie voor informatie over andere functies van premium-cache, [inleiding toohello Azure Redis-Cache Premium-laag](cache-premium-tier-intro.md).

## <a name="what-is-data-persistence"></a>Wat is gegevenspersistentie?
[Redis-persistentie](https://redis.io/topics/persistence) kunt u toopersist opgeslagen gegevens in Redis. U kunt ook momentopnamen en back-up Hallo-gegevens die u in het geval van een hardwarefout laden kunt. Dit is een grote voordeel ten opzichte van Basic of standaardcategorie waarbij alle gegevens Hallo wordt opgeslagen in het geheugen en kunnen er mogelijk gegevensverlies in geval van een storing waar Cache-knooppunten niet beschikbaar zijn. 

Azure Redis-Cache biedt Redis-persistentie met Hallo modellen te volgen:

* **RDB persistentie** -persistentie wanneer RDB (Redis database) is geconfigureerd, Azure Redis-Cache een momentopname van Redis-cache in een binaire indeling toodisk op basis van een configureerbare back-upfrequentie Redis Hallo blijft bestaan. Als er een onherstelbare gebeurtenis optreedt die zowel Hallo primaire en replica cache uitgeschakeld, is Hallo cache opnieuw met de meest recente momentopname Hallo samengesteld. Meer informatie over Hallo [voordelen](https://redis.io/topics/persistence#rdb-advantages) en [nadelen](https://redis.io/topics/persistence#rdb-disadvantages) van RDB persistentie.
* **AOF persistentie** -persistentie wanneer AOF (alleen Append-bestand) is geconfigureerd, Azure Redis-Cache worden opgeslagen voor elke schrijven tooa bewerkingslogboek dat ten minste eenmaal per seconde bij een Azure Storage-account is opgeslagen. Als er een onherstelbare gebeurtenis optreedt die zowel Hallo primaire en replica cache uitgeschakeld, is Hallo cache opnieuw samengesteld met behulp van schrijfbewerkingen Hallo opgeslagen. Meer informatie over Hallo [voordelen](https://redis.io/topics/persistence#aof-advantages) en [nadelen](https://redis.io/topics/persistence#aof-disadvantages) van AOF persistentie.

Persistentie wordt geconfigureerd via Hallo **nieuwe Redis-Cache** blade tijdens het maken van de cache en op Hallo **Resource menu** voor bestaande premium in de cache opslaat.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Nadat een premium-prijscategorie is geselecteerd, klikt u op **Redis-persistentie**.

![Redis-persistentie][redis-cache-persistence]

Hallo stappen in de volgende sectie Hallo Beschrijf hoe tooconfigure Redis-persistentie op uw nieuwe premium-cache. Zodra de Redis-persistentie is geconfigureerd, klikt u op **maken** toocreate uw nieuwe premium in de cache met Redis-persistentie.

## <a name="enable-redis-persistence"></a>Redis-persistentie inschakelen

Redis-persistentie is ingeschakeld op Hallo **Redis-gegevenspersistentie** blade door het kiezen van een **RDB** of **AOF** persistentie. Deze blade wordt voor nieuwe caches geopend tijdens het Hallo-cache maken, zoals beschreven in de vorige sectie Hallo. Voor bestaande caches Hallo **Redis-gegevenspersistentie** blade wordt geopend vanuit Hallo **Resource menu** voor uw cache.

![Instellingen voor redis][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>RDB persistentie configureren

tooenable RDB persistentie, klikt u op **RDB**. toodisable RDB persistentie op een eerder ingeschakelde premium-cache, klikt u op **uitgeschakelde**.

![Redis-persistentie RDB][redis-cache-rdb-persistence]

tooconfigure hello back-up-interval, selecteer een **back-upfrequentie** uit de vervolgkeuzelijst Hallo. U kunt kiezen uit **15 minuten**, **30 minuten**, **60 minuten**, **6 uur**, **12 uur**, en **24 uur**. Dit interval begint te tellen omlaag nadat Hallo eerdere back-upbewerking is voltooid en wanneer deze is verstreken een nieuwe back-up wordt gestart.

Klik op **Opslagaccount** tooselect Hallo storage account toouse en kies ofwel Hallo **primaire sleutel** of **secundaire sleutel** toouse van Hallo **opslag Sleutel** vervolgkeuzelijst. U moet een opslagaccount kiezen in Hallo dezelfde regio bevinden als het Hallo-cache, en een **Premium-opslag** account wordt aanbevolen omdat premium-opslag heeft een hogere doorvoer. 

> [!IMPORTANT]
> Als Hallo-opslagsleutel voor uw account persistentie wordt opnieuw gegenereerd, moet u de gewenste sleutel Hallo in Hallo configureren **opslagsleutel** vervolgkeuzelijst.
> 
> 

Klik op **OK** toosave Hallo persistentie configuratie.

Hallo volgende back-up (of eerste back-up voor nieuwe caches) wordt gestart zodra hello back-upfrequentie-interval is verstreken.

## <a name="configure-aof-persistence"></a>AOF persistentie configureren

tooenable AOF persistentie, klikt u op **AOF**. toodisable AOF persistentie op een eerder ingeschakelde premium-cache, klikt u op **uitgeschakelde**.

![Redis-persistentie AOF][redis-cache-aof-persistence]

tooconfigure AOF persistentie, Geef een **eerste Opslagaccount**. Dit opslagaccount moet Hallo dezelfde regio bevinden als het Hallo-cache, en een **Premium-opslag** account wordt aanbevolen omdat premium-opslag heeft een hogere doorvoer. U kunt desgewenst een extra storage-account met de naam **tweede Opslagaccount**. Als een tweede storage-account is geconfigureerd, hello schrijfbewerkingen toohello replica cache worden geschreven toothis tweede storage-account. Kies voor elke geconfigureerde opslagaccount beide Hallo **primaire sleutel** of **secundaire sleutel** toouse van Hallo **opslagsleutel** vervolgkeuzelijst. 

> [!IMPORTANT]
> Als Hallo-opslagsleutel voor uw account persistentie wordt opnieuw gegenereerd, moet u de gewenste sleutel Hallo in Hallo configureren **opslagsleutel** vervolgkeuzelijst.
> 
> 

Wanneer de persistentie AOF is ingeschakeld, schrijven operations toohello cache toohello aangewezen storage-account (of accounts als u een tweede storage-account hebt geconfigureerd) worden opgeslagen. In geval van een onherstelbare fout Hallo gebruikt dat vindt u beide Hallo primaire en replica-cache, hello opgeslagen AOF logboek is toorebuild Hallo cache.

## <a name="persistence-faq"></a>Persistentie Veelgestelde vragen
Hallo bevat volgende lijst toocommonly van antwoorden op veelgestelde vragen over Azure Redis-Cache persistentie.

* [Kan ik persistentie op een eerder gemaakte cache inschakelen?](#can-i-enable-persistence-on-a-previously-created-cache)
* [Kan ik AOF en RDB persistentie op Hallo inschakelen hetzelfde moment?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [Welk model persistentie moet ik kiezen?](#which-persistence-model-should-i-choose)
* [Wat gebeurt er als ik tooa andere grootte hebt aangepast en een back-up is hersteld die is gemaakt voordat de bewerking schalen Hallo?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>RDB persistentie
* [Kan ik Hallo RDB back-upfrequentie wijzigen nadat het maken van Hallo-cache?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [Waarom als ik een back-upfrequentie RDB van 60 minuten er meer dan 60 minuten tussen back-ups is?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [Wat gebeurt er toohello oude RDB back-ups wanneer een nieuwe back-up wordt gemaakt?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>AOF persistentie
* [Wanneer moet ik een tweede storage-account gebruiken?](#when-should-i-use-a-second-storage-account)
* [Ondersteunt AOF persistentie invloed in de gehele, latentie, of de prestaties van mijn cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [Hoe kan ik Hallo tweede storage-account verwijderen?](#how-can-i-remove-the-second-storage-account)
* [Wat is er een herschrijven en wat betekent dat voor mijn cache?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [Wat moet ik verwachten tijdens het schalen van een cache met AOF ingeschakeld?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [Hoe wordt mijn gegevens AOF ingedeeld in de opslag?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>Kan ik persistentie op een eerder gemaakte cache inschakelen?
Ja, Redis-persistentie kan worden geconfigureerd op de cache maken en bestaande premium in de cache van.

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>Kan ik AOF en RDB persistentie op Hallo inschakelen hetzelfde moment?

Nee, kunt u alleen RDB of AOF, maar niet beide op Hallo inschakelen hetzelfde moment.

### <a name="which-persistence-model-should-i-choose"></a>Welk model persistentie moet ik kiezen?

AOF persistentie slaat elke schrijven tooa logboek enkele invloed op de doorvoer heeft, vergeleken met RDB persistentie waarin wordt opgeslagen back-ups op basis van Hallo back-interval geconfigureerd met minimale gevolgen voor prestaties. Kies AOF persistentie als het primaire doel toominimize gegevensverlies, en u een afname in doorvoer voor uw cache verwerken kunt. Kies RDB persistentie als u wilt dat de optimale doorvoer toomaintain op uw cache, maar toch een mechanisme om gegevens te herstellen.

* Meer informatie over Hallo [voordelen](https://redis.io/topics/persistence#rdb-advantages) en [nadelen](https://redis.io/topics/persistence#rdb-disadvantages) van RDB persistentie.
* Meer informatie over Hallo [voordelen](https://redis.io/topics/persistence#aof-advantages) en [nadelen](https://redis.io/topics/persistence#aof-disadvantages) van AOF persistentie.

Zie voor meer informatie over prestaties bij gebruik van AOF persistentie [biedt AOF persistentie invloed in de gehele, latentie, of de prestaties van mijn cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>Wat gebeurt er als ik tooa andere grootte hebt aangepast en een back-up is hersteld die is gemaakt voordat de bewerking schalen Hallo?

Voor zowel RDB AOF persistentie:

* Als u de schaal groter tooa hebt aangepast, zijn er geen gevolgen.
* Als u kleinere tooa hebt geschaald, en u een aangepaste hebt [databases](cache-configure.md#databases) instelling die groter is dan Hallo [databases limiet](cache-configure.md#databases) voor de grootte van uw nieuwe gegevens in deze databases is niet hersteld. Zie voor meer informatie [Mijn aangepaste databases betrokken instellen tijdens het schalen Is?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Als u kleinere tooa hebt geschaald en er niet genoeg ruimte in Hallo kleinere grootte toohold alle gegevens van de laatste back-up, sleutels Hallo Hallo onbeschikbaar tijdens het terugzetten van een hello gemaakt wordt, meestal met behulp van Hallo [allkeys lru](http://redis.io/topics/lru-cache) verwijderen het beleid.

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>Kan ik Hallo RDB back-upfrequentie wijzigen nadat het maken van Hallo-cache?
Ja, kunt u back-upfrequentie voor persistentie RDB op Hallo Hallo **Redis-gegevenspersistentie** blade. Zie voor instructies [configureren Redis-persistentie](#configure-redis-persistence).

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>Waarom als ik een back-upfrequentie RDB van 60 minuten er meer dan 60 minuten tussen back-ups is?
Hallo RDB persistentie back-upfrequentie interval start niet totdat de vorige back-upproces Hallo is voltooid. Als de back-upfrequentie Hallo is 60 minuten duurt een volledige back-upproces 15 minuten toosuccessfully, start Hallo volgende back-up niet totdat 75 minuten nadat de Hallo begintijd van Hallo eerdere back-up.

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>Wat gebeurt er toohello oude RDB back-ups wanneer een nieuwe back-up wordt gemaakt?
Alle RDB persistentie back-ups met uitzondering van de meest recente Hallo worden automatisch verwijderd. Deze verwijdering mogelijk niet direct plaats, maar oudere back-ups zijn niet voor onbepaalde tijd bewaard.


### <a name="when-should-i-use-a-second-storage-account"></a>Wanneer moet ik een tweede storage-account gebruiken?

Als u denkt dat u hoger dan de verwachte set bewerkingen op Hallo-cache hebt, moet u een tweede storage-account voor AOF persistentie.  Instellen van de secundaire opslagaccount Hallo zorgt ervoor dat uw cache opslaglimieten van bandbreedte niet bereiken.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>Ondersteunt AOF persistentie invloed in de gehele, latentie, of de prestaties van mijn cache?

AOF persistentie is van invloed op doorvoer door ongeveer 15% – 20% wanneer Hallo cache lager dan de maximale belasting is (CPU- en laden beide onder 90%). Er mag niet zijn latentieproblemen bij het Hallo-cache is binnen dit bereik. Echter Hallo cache tot komen deze limieten sneller met AOF ingeschakeld.

### <a name="how-can-i-remove-hello-second-storage-account"></a>Hoe kan ik Hallo tweede storage-account verwijderen?

U kunt Hallo AOF persistentie secundaire storage-account verwijderen door in te stellen Hallo tweede opslagaccount toobe Hallo dezelfde als de eerste opslagaccount Hallo. Zie voor instructies [AOF configureren persistentie](#configure-aof-persistence).

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>Wat is er een herschrijven en wat betekent dat voor mijn cache?

Als Hallo AOF bestand erg groot genoeg is, een herschrijven wordt automatisch in de wachtrij op Hallo-cache. Hallo herschrijven voorkeursoptie Hallo AOF bestand met minimale set Hallo van bewerkingen die nodig zijn toocreate Hallo huidige gegevensset. Tijdens de regeneraties, verwachten dat tooreach prestatielimieten sneller vooral wanneer omgaan met grote gegevenssets. Regeneraties optreden minder vaak zoals Hallo AOF bestand groter wordt, maar duurt een aanzienlijke hoeveelheid tijd wanneer dit gebeurt.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>Wat moet ik verwachten tijdens het schalen van een cache met AOF ingeschakeld?

Als Hallo AOF gelijktijdig Hallo met schalen aanzienlijk groot is, klikt u vervolgens verwachten dat Hallo scale bewerking tootake langer dan verwacht, omdat deze wordt opnieuw Hallo bestand nadat het schalen is voltooid.

Zie voor meer informatie over het schalen [wat gebeurt er als ik tooa andere grootte hebt aangepast en een back-up is hersteld die is gemaakt voordat de bewerking schalen Hallo?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>Hoe wordt mijn gegevens AOF ingedeeld in de opslag?

Gegevens die zijn opgeslagen in AOF bestanden is onderverdeeld in meerdere pagina-blobs per knooppunt tooincrease prestaties Hallo gegevens toostorage op te slaan. Hallo volgende tabel geeft weer hoeveel pagina-BLOB's worden gebruikt voor elke prijscategorie:

| Premiumlaag | Blobs |
|--------------|-------|
| P1           | 4 per shard    |
| P2           | 8 per shard    |
| P3           | 16 per shard   |
| P4           | 20 per shard   |

Wanneer clustering is ingeschakeld, heeft elke shard in Hallo-cache een eigen set van pagina-blobs, zoals aangegeven in de vorige tabel Hallo. Een cache P2 met drie shards verdeelt bijvoorbeeld het bestand AOF over 24 pagina-blobs (8 BLOB's per shard met 3 shards).

Na een herschrijven bestaan twee sets van AOF bestanden in de opslag. Regeneraties optreden in Hallo achtergrond en toevoeg-toohello eerste set van bestanden, terwijl de set-bewerkingen voor die cache toohello worden verzonden tijdens het Hallo herschrijven toohello tweede set toevoegen. Een back-up wordt tijdelijk opgeslagen tijdens regeneraties in geval van storing, maar onmiddellijk is verwijderd nadat een herschrijven is voltooid.


## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe meer premium toouse functies in de cache.

* [Inleiding toohello Azure Redis-Cache Premium-laag](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
