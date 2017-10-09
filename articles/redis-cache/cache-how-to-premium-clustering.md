---
title: aaaHow tooconfigure Redis clustering voor een Premium Azure Redis-Cache | Microsoft Docs
description: Meer informatie over hoe toocreate en beheren van Redis-clustering voor de laag Premium Azure Redis-Cache-exemplaren
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Hoe tooconfigure Redis clustering voor een Premium Azure Redis-Cache
Azure Redis-Cache heeft verschillende cache aanbiedingen die flexibiliteit bij het Hallo-keuze van de cachegrootte en -onderdelen bieden, met inbegrip van Premium-laag functies zoals clustering, persistentie en virtual network-ondersteuning. Dit artikel wordt beschreven hoe tooconfigure clustering van een premium Azure Redis-Cache exemplaar.

Zie voor informatie over andere functies van premium-cache, [inleiding toohello Azure Redis-Cache Premium-laag](cache-premium-tier-intro.md).

## <a name="what-is-redis-cluster"></a>Wat is de Redis-Cluster?
Azure Redis-Cache biedt Redis-cluster als [geïmplementeerd in Redis](http://redis.io/topics/cluster-tutorial). Met Redis-Cluster beschikt u over Hallo volgende voordelen: 

* Hallo mogelijkheid tooautomatically splitsen uw gegevensset tussen meerdere knooppunten. 
* Hallo mogelijkheid toocontinue bewerkingen wanneer een subset van Hallo knooppunten ondervindt fouten of kan geen toocommunicate met rest Hallo van Hallo cluster zijn. 
* Meer doorvoer: doorvoer lineair neemt toe naarmate u Hallo aantal shards verhogen. 
* Grootte van meer geheugen: Lineair neemt toe naarmate u Hallo aantal shards verhogen.  

Zie voor meer informatie over de grootte, doorvoer en bandbreedte van premiumcaches [welke aanbieding Redis-Cache en de grootte moet ik gebruiken?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

In Azure wordt Redis-cluster aangeboden als een primair/replica model waarin de elke shard heeft een paar primair/replica met replicatie waar Hallo replicatie wordt beheerd door service van Azure Redis-Cache. 

## <a name="clustering"></a>Clustering
Clustering is ingeschakeld op Hallo **nieuwe Redis-Cache** blade tijdens het maken van de cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Clustering is geconfigureerd op Hallo **Redis-Cluster** blade.

![Clustering][redis-cache-clustering]

U kunt hebben up too10 shards in Hallo-cluster. Klik op **ingeschakeld** en schuift Hallo schuifregelaar of typ een getal tussen 1 en 10 voor **Shard aantal** en klik op **OK**.

Elke shard is een primair/replica cache paar beheerd door Azure en Hallo totale grootte van de cache Hallo wordt vermenigvuldigd Hallo aantal shards Hallo cachegrootte is geselecteerd in Hallo prijscategorie. 

![Clustering][redis-cache-clustering-selected]

Zodra het Hallo-cache wordt gemaakt u tooit verbinding maken met en gebruik deze net zoals een niet-geclusterde cache en Redis distribueert Hallo gegevensdoorvoer Hallo Cache shards. Als u diagnostische gegevens is [ingeschakeld](cache-how-to-monitor.md#enable-cache-diagnostics), metrische gegevens voor elke shard afzonderlijk worden vastgelegd en kunnen worden [bekeken](cache-how-to-monitor.md) hello Redis-Cache-blade. 

> [!NOTE]
> 
> Er zijn een aantal kleine verschillen in de clienttoepassing vereist wanneer clustering is geconfigureerd. Zie voor meer informatie [heb ik nodig toomake eventuele wijzigingen toomy client toepassing toouse clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Zie voor voorbeeldcode over het werken met clustering met de client StackExchange.Redis Hallo Hallo [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) gedeelte Hallo [Hallo wereld](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) voorbeeld.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>De clustergrootte Hallo op een actieve wijzigen premium-cache
toochange hello clustergrootte op een actieve premium in de cache met clustering en klik **clustergrootte Redis** van Hallo **Resource menu**.

> [!NOTE]
> Terwijl hello Azure Redis-Cache Premium laag is vrijgegeven tooGeneral beschikbaarheid, is Hallo clustergrootte Redis-functie momenteel preview.
> 
> 

![Clustergrootte redis][redis-cache-redis-cluster-size]

Hallo clustergrootte toochange gebruik Hallo schuifregelaar of typ een getal tussen 1 en 10 in Hallo **Shard aantal** tekstvak en klik op **OK** toosave.

> [!NOTE]
> Schalen van een cluster wordt uitgevoerd Hallo [migreren](https://redis.io/commands/migrate) opdracht, die een dure opdracht, dus voor minimale invloed, kunt u deze bewerking tijdens daluren uitvoert. Tijdens het migratieproces hello ziet u een piek in de belasting van de server. Schalen van een cluster wordt uitgevoerd een lang proces en Hallo hoeveelheid tijd is afhankelijk van Hallo aantal sleutels en de grootte van Hallo waarden die zijn gekoppeld aan deze sleutels.
> 
> 

## <a name="clustering-faq"></a>Veelgestelde vragen over clustering
Hallo bevat volgende lijst toocommonly van antwoorden op veelgestelde vragen over Azure Redis-Cache clustering.

* [Moet ik toomake eventuele wijzigingen toomy client toepassing toouse clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [Hoe worden de sleutels in een cluster gedistribueerd?](#how-are-keys-distributed-in-a-cluster)
* [Wat is Hallo grootste cachegrootte die ik kan maken?](#what-is-the-largest-cache-size-i-can-create)
* [Alle Redis-clients ondersteunen clustering?](#do-all-redis-clients-support-clustering)
* [Hoe kan ik toomy cache verbinden wanneer clustering is ingeschakeld?](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [Kan ik afzonderlijke shards toohello van mijn cache rechtstreeks verbinden?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [Kan ik de clustering voor een eerder gemaakte cache configureren?](#can-i-configure-clustering-for-a-previously-created-cache)
* [Kan ik de clustering voor een basis of standaard-cache configureren?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [Kan ik de clustering met Hallo Redis ASP.NET Session State en uitvoercaching-providers gebruiken?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [Ik krijg verplaatsen uitzonderingen bij gebruik van StackExchange.Redis en clustering, wat moet ik doen?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>Moet ik toomake eventuele wijzigingen toomy client toepassing toouse clustering?
* Wanneer clustering is ingeschakeld, wordt alleen database 0 beschikbaar is. Als uw clienttoepassing gebruikmaakt van meerdere databases en wordt geprobeerd een tooread- of schrijfbewerking tooa andere database dan 0, hello volgende uitzondering is opgetreden. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  Zie voor meer informatie [clusterspecificatie Redis - geïmplementeerde subset](http://redis.io/topics/cluster-spec#implemented-subset).
* Als u [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), moet u 1.0.481 of hoger. U toohello cache verbinding maken met behulp van dezelfde Hallo [eindpunten, poorten en sleutels](cache-configure.md#properties) waarmee u verbinding maakt tooa-cache geen clusteren is ingeschakeld heeft. Hallo enige verschil is dat alle lees- en schrijfbewerkingen moeten worden uitgevoerd toodatabase 0.
  
  * Andere clients mogelijk andere vereisten. Zie [alle Redis-clients ondersteunen clustering?](#do-all-redis-clients-support-clustering)
* Als uw toepassing gebruikmaakt van meerdere sleutelbewerkingen batch worden opgenomen in één opdracht, alle sleutels moeten zich bevinden in Hallo dezelfde shard. toolocate sleutels in dezelfde shard Hallo, Zie [hoe worden sleutels verdeeld in een cluster?](#how-are-keys-distributed-in-a-cluster)
* Als u van ASP.NET Session State-provider Redis gebruikmaakt moet u 2.0.1 of hoger. Zie [kan ik gebruiken met de ASP.NET-sessiestatus Redis en uitvoercaching providers Hallo clustering?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>Hoe worden de sleutels in een cluster gedistribueerd?
Per Hallo Redis [sleutels distributiemodel](http://redis.io/topics/cluster-spec#keys-distribution-model) documentatie: key ruimte Hallo 16384 sleuven opgesplitst. Elke sleutel wordt gehasht en tooone deze sleuven, zijn verdeeld over knooppunten Hallo van Hallo cluster toegewezen. U kunt configureren die deel van het Hallo-sleutel is hash tooensure die meerdere sleutels bevinden zich in dezelfde shard met hash-tags Hallo.

* Met een hash-code - sleutels als een deel van het Hallo-sleutel is ingesloten in `{` en `}`, alleen deel van het Hallo-sleutel wordt opgedeeld voor Hallo Hallo hash sleuf van een sleutel vaststellen van. Bijvoorbeeld, Hallo 3 sleutels volgen zou bevinden in Hallo dezelfde shard: `{key}1`, `{key}2`, en `{key}3` sinds alleen Hallo `key` deel van naam hello wordt opgedeeld. Zie voor een volledige lijst met sleutels hash-code specificaties [sleutels hash-tags](http://redis.io/topics/cluster-spec#keys-hash-tags).
* Sleutels zonder een hash-code - Hallo gehele sleutelnaam wordt gebruikt voor de hash. Dit resulteert in een statistisch gelijkmatige verdeling over Hallo shards Hallo-cache.

Voor optimale prestaties en doorvoer te Hallo sleutels gelijkmatig verdelen. Als u van sleutels met een hash-code gebruikmaakt is van de toepassing hello verantwoordelijkheid tooensure Hallo sleutels gelijkmatig worden gedistribueerd.

Zie voor meer informatie [sleutels distributiemodel](http://redis.io/topics/cluster-spec#keys-distribution-model), [Redis-Cluster gegevens sharding](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding), en [sleutels hash-tags](http://redis.io/topics/cluster-spec#keys-hash-tags).

Dezelfde shard met Hallo StackExchange.Redis client, Zie Hallo voor voorbeeldcode over het werken met clustering en sleutels in Hallo vinden [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) gedeelte Hallo [Hallo wereld](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) voorbeeld.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>Wat is Hallo grootste cachegrootte die ik kan maken?
grootste premium Hallo-cachegrootte is 53 GB. U kunt maken van too10 shards zodat u een maximale grootte van 530 GB. Als u een groter formaat moet kunt u [aanvragen meer](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). Zie voor meer informatie [prijzen van Azure Redis-Cache](https://azure.microsoft.com/pricing/details/cache/).

### <a name="do-all-redis-clients-support-clustering"></a>Alle Redis-clients ondersteunen clustering?
Op Hallo Redis dit moment die niet alle clients ondersteunen clustering. StackExchange.Redis is een versie die ondersteuning biedt voor. Zie voor meer informatie over andere clients Hallo [met Hallo cluster speelt](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) sectie Hallo [Redis-cluster zelfstudie](http://redis.io/topics/cluster-tutorial).

> [!NOTE]
> Als u StackExchange.Redis gebruikt als de client, controleert u met behulp van de meest recente versie Hallo van [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 of hoger voor clustering toowork correct. Als u problemen met verplaatsen uitzonderingen hebt, raadpleegt u [uitzonderingen verplaatsen](#move-exceptions) voor meer informatie.
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>Hoe kan ik toomy cache verbinden wanneer clustering is ingeschakeld?
U kunt verbinding maken tooyour cache met behulp van dezelfde Hallo [eindpunten](cache-configure.md#properties), [poorten](cache-configure.md#properties), en [sleutels](cache-configure.md#access-keys) waarmee u verbinding maakt tooa-cache geen clusteren is ingeschakeld heeft. Redis hello clustering op Hallo backend, zodat er geen toomanage beheert via de client.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>Kan ik afzonderlijke shards toohello van mijn cache rechtstreeks verbinden?
Dit wordt niet officieel ondersteund. Met die gezegd, wordt elke shard bestaat uit de cache combinatie van een primair/replica, gezamenlijk aangeduid als een cache-exemplaar. U kunt verbinding maken toothese cache-exemplaren die gebruikmaken van Hallo redis cli-hulpprogramma in Hallo [onstabiel](http://redis.io/download) branche van Hallo Redis-opslagplaats op GitHub. Deze versie implementeert basisondersteuning wanneer gestart met de Hallo `-c` overschakelen. Zie voor meer informatie [met Hallo cluster speelt](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) op [http://redis.io](http://redis.io) in Hallo [Redis-cluster zelfstudie](http://redis.io/topics/cluster-tutorial).

Voor niet-ssl gebruiken Hallo opdrachten te volgen.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

Voor ssl, vervangt u `1300N` met `1500N`.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>Kan ik de clustering voor een eerder gemaakte cache configureren?
U kunt momenteel alleen inschakelen wanneer u een cache maken clustering. U kunt de clustergrootte Hallo wijzigen nadat Hallo-cache wordt gemaakt, maar kunt u premium-cache voor clustering tooa toevoegen of verwijderen uit de cache premium clustering nadat het Hallo-cache wordt gemaakt. Een premium-cache met clusteren is ingeschakeld en slechts één shard is anders dan een premium-cache van Hallo dezelfde met geen clustering grootte.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>Kan ik de clustering voor een basis of standaard-cache configureren?
Clustering is alleen beschikbaar voor premium-caches.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>Kan ik de clustering met Hallo Redis ASP.NET Session State en uitvoercaching-providers gebruiken?
* **Redis-Cache-uitvoer provider** -er zijn geen wijzigingen vereist.
* **Redis Session State-provider** -toouse clustering, moet u [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 of hoger, of een uitzondering gegenereerd. Dit is een belangrijke wijziging; Zie voor meer informatie [v2.0.0 Details van de wijziging op te splitsen](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>Ik krijg verplaatsen uitzonderingen bij gebruik van StackExchange.Redis en clustering, wat moet ik doen?
Als u van StackExchange.Redis gebruikmaakt en ontvangt `MOVE` uitzonderingen bij gebruik van clustering, zorg ervoor dat u gebruikmaakt van [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) of hoger. Zie voor instructies over het configureren van uw .NET-toepassingen toouse StackExchange.Redis [hello cacheclients configureren](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe meer premium toouse functies in de cache.

* [Inleiding toohello Azure Redis-Cache Premium-laag](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







