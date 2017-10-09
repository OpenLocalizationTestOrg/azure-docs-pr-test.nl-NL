---
title: aaaMigrate Managed Cache Service toepassingen tooRedis - Azure | Microsoft Docs
description: Meer informatie over hoe toomigrate Managed Cache Service en In-Role Cache toepassingen tooAzure Redis-Cache
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>Migreren van Managed Cache Service tooAzure Redis-Cache
Migreren van uw toepassingen die gebruikmaken van Azure Managed Cache Service tooAzure Redis-Cache kan worden bewerkstelligd met minimale wijzigingen tooyour toepassing, afhankelijk van Hallo Managed Cache Service functies die worden gebruikt door uw toepassing in het cachegeheugen. Hoewel Hallo API's zijn niet precies Hallo dezelfde ze zijn vergelijkbaar en veel van de bestaande code die gebruikmaakt van Managed Cache Service tooaccess een cache met minimale wijzigingen opnieuw kan worden gebruikt. In dit onderwerp toont hoe toomake Hallo nodig configuratie en toepassing verandert toomigrate uw Managed Cache Service toepassingen toouse Azure Redis-Cache en ziet u hoe aantal Hallo functies van Azure Redis-Cache gebruikte tooimplement Hallo functionaliteit kan zijn een Managed Cache Service-cache.

>[!NOTE]
>Beheerde Cache Service en In-Role Cache waren [buiten gebruik gesteld](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) 30 November 2016. Als u een In-Role Cache-implementaties die u wilt dat toomigrate tooAzure Redis-Cache hebt, kunt u de stappen in dit artikel Hallo volgen.

## <a name="migration-steps"></a>Stappen voor migratie
Hallo stappen zijn vereist toomigrate een Managed Cache Service toepassing toouse Azure Redis-Cache.

* Toewijzen van Managed Cache Service functies tooAzure Redis-Cache
* Kies een Cache-aanbieding
* Een Cache maken
* Hallo-Cacheclients configureren
  * Hallo Managed Cache Service-configuratie verwijderen
  * Een cacheclient met behulp van Hallo NuGet-pakket StackExchange.Redis configureren
* Managed Cache Service code migreren
  * Verbinding maken met behulp van Hallo ConnectionMultiplexer klasse toohello-cache
  * De primitieve gegevenstypen toegang in Hallo-cache
  * Werken met .NET-objecten in cache Hallo
* ASP.NET-sessiestatus en tooAzure Redis-Cache van de uitvoercache migreren 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>Toewijzen van Managed Cache Service functies tooAzure Redis-Cache
Azure Managed Cache Service en Azure Redis-Cache zijn vergelijkbaar, maar sommige functies op verschillende manieren implementeren. Deze sectie worden enkele van Hallo verschillen beschreven en vindt u informatie op het Hallo-functies van Managed Cache Service implementeren in Azure Redis-Cache.

| Beheerde onderdeel van de Cache Service | Ondersteuning van beheerde Cache Service | Ondersteuning van Azure Redis-Cache |
| --- | --- | --- |
| Benoemde caches |Een standaardcache is geconfigureerd en in Hallo Standard en Premium-cache-aanbiedingen, van aanvullende toonine caches met de naam kunnen worden geconfigureerd als gewenst. |Azure Redis-caches hebben een configureerbare aantal databases (standaard van 16) die kunnen worden gebruikt tooimplement een vergelijkbare functionaliteit toonamed in de cache opslaat. Zie [Wat zijn Redis-databases?](cache-faq.md#what-are-redis-databases) en [Standaardconfiguratie voor Redis-server](cache-configure.md#default-redis-server-configuration) voor meer informatie. |
| Hoge beschikbaarheid |Biedt hoge beschikbaarheid voor items in de cache Hallo in het Hallo Standard en Premium-cache-aanbiedingen. Als items verbroken vanwege tooa mislukt zijn, kan back-ups van items in de cache Hallo Hallo nog steeds beschikbaar. Schrijft toohello secundaire cache synchroon worden aangebracht. |Hoge beschikbaarheid is beschikbaar in Hallo Standard en Premium-cache-aanbiedingen, waarvoor een twee knooppunten (primair/Replica)-configuratie (elke shard in een Premium-cache heeft een paar primair/replica). Schrijfbewerkingen toohello replica asynchroon worden gedaan. Zie voor meer informatie [prijzen van Azure Redis-Cache](https://azure.microsoft.com/pricing/details/cache/). |
| Meldingen |U kunt clients tooreceive asynchrone meldingen wanneer een aantal cachebewerkingen plaatsvinden op een benoemde cache. |Clienttoepassingen kunnen gebruikmaken van Redis pub subitems of [Keyspace-kennisgevingen](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve een vergelijkbare functionaliteit toonotifications. |
| Lokale cache |Lokaal een kopie van de objecten in de cache opgeslagen op Hallo van client voor extra snelle toegang. |Clienttoepassingen moet tooimplement deze functionaliteit met behulp van een woordenboek of vergelijkbare gegevensstructuur. |
| Beleid verwijderen |Geen of LRU. Hallo-standaardbeleid is LRU. |Azure Redis-Cache ondersteunt de volgende taakverwijdering beleidsregels Hallo: vluchtige lru, allkeys lru, vluchtige willekeurige, allkeys-willekeurige vluchtige-ttl, noeviction. Hallo-standaardbeleid is vluchtige lru. Zie voor meer informatie [serverconfiguratie standaard Redis](cache-configure.md#default-redis-server-configuration). |
| Een verloopbeleid voor |Hallo standaard verloopbeleid is Absolute en Hallo verlopen interval is standaard tien minuten. Bij Verschuivend en nooit beleidsregels zijn ook beschikbaar. |Standaard-items in de cache Hallo niet verlopen, maar een vervaldatum kan worden geconfigureerd op basis van per schrijven met behulp van de cache set overloads. Zie voor meer informatie [objecten toevoegen en ophalen uit de cache Hallo](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache). |
| Regio's en labels |Gebieden zijn subgroepen voor in de cache-items. Regio's bieden ook ondersteuning voor Hallo aantekening van items in de cache met extra beschrijvende tekenreeksen labels genoemd. Regio's ondersteunen Hallo mogelijkheid tooperform zoekopdrachten met tags objecten in deze regio. Alle items in een regio bevinden zich in één knooppunt van Hallo cache-cluster. |Een Redis-cache bestaat uit één knooppunt, (tenzij de Redis-cluster is ingeschakeld) zodat Hallo concept van Managed Cache Service regio's is niet van toepassing. Redis ondersteunt zoeken en jokerteken bewerkingen bij het ophalen van sleutels, zodat beschrijvende tags kunnen worden ingesloten in de sleutelnamen hello later tooretrieve Hallo items gebruikt. Zie voor een voorbeeld van de implementatie van een tagging oplossing met behulp van Redis [uitvoering van labels met Redis cache](http://stackify.com/implementing-cache-tagging-redis/). |
| Serialisatie |Managed Cache ondersteunt NetDataContractSerializer, BinaryFormatter en Hallo gebruik van aangepaste objectserializers. Hallo standaardwaarde is NetDataContractSerializer. |Het is Hallo verantwoordelijkheid van Hallo client tooserialize .NET toepassingsobjecten voordat ze worden geplaatst in de cache hello, met Hallo keuze Hallo serialisatiefunctie up toepassingsontwikkelaar toohello-client. Zie voor meer informatie en voorbeeldcode [werken met .NET-objecten in cache Hallo](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache). |
| Cache-emulator |Managed Cache biedt de emulator van een lokale cache. |Azure Redis-Cache heeft geen een emulator, maar u kunt [hello MSOpenTech build van redis-server.exe lokaal uitvoeren](cache-faq.md#cache-emulator) tooprovide een emulator ervaring. |

## <a name="choose-a-cache-offering"></a>Kies een Cache-aanbieding
Microsoft Azure Redis-Cache is beschikbaar in Hallo lagen te volgen:

* **Basic**: één knooppunt. Meerdere groottes van too53 GB.
* **Standard**: twee knooppunten (primair/replica). Meerdere groottes van too53 GB. 99,9% SLA.
* **Premium** : twee knooppunten primair/Replica met up too10 shards. Meerdere groottes van 6 GB too530 GB. Alle functies van de lagen Standard en Premium bieden ondersteuning voor [Redis-cluster](cache-how-to-premium-clustering.md), [Redis-persistentie](cache-how-to-premium-persistence.md) en [Azure Virtual Network](cache-how-to-premium-vnet.md). 99,9% SLA.

Elke laag verschilt wat functies en prijzen betreft. Hallo functies vallen verderop in deze handleiding en voor meer informatie over prijzen, Zie [prijsdetails voor caches](https://azure.microsoft.com/pricing/details/cache/).

Een startpunt voor de migratie is toopick Hallo grootte die overeenkomt met de Hallo omvang van de vorige Managed Cache Service-cache en vervolgens omhoog of omlaag schalen, afhankelijk van de vereisten van uw toepassing hello. Zie voor meer informatie over het kiezen van het juiste Azure Redis-Cache aanbieding Hallo [welke aanbieding Redis-Cache en de grootte moet ik gebruiken?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="create-a-cache"></a>Een Cache maken
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Hallo-Cacheclients configureren
Zodra het Hallo-cache is gemaakt en geconfigureerd, de volgende stap Hallo tooremove Hallo Managed Cache Service configuratie en Hallo toevoegen hello Azure Redis-Cache-configuratie en verwijzingen toevoegen zodat cacheclients toegang Hallo-cache tot hebben.

* Hallo Managed Cache Service-configuratie verwijderen
* Een cacheclient met behulp van Hallo NuGet-pakket StackExchange.Redis configureren

### <a name="remove-hello-managed-cache-service-configuration"></a>Hallo Managed Cache Service-configuratie verwijderen
Voordat u Hallo clienttoepassingen kunnen worden geconfigureerd voor Azure Redis-Cache, Hallo bestaande Managed Cache Service configuratie en assembly-verwijzingen moeten worden verwijderd met het verwijderen van Hallo Managed Cache Service NuGet-pakket.

toouninstall hello Managed Cache Service NuGet-pakket met de rechtermuisknop op de client-project in Hallo **Solution Explorer** en kies **NuGet-pakketten beheren**. Selecteer Hallo **geïnstalleerde pakketten** -knooppunt en typ W**indowsAzure.Caching** in Hallo zoeken pakketten vak geïnstalleerd. Selecteer **Windows** **Azure Cache** (of **Windows** **Azure Caching** afhankelijk van de versie Hallo van Hallo NuGet-pakket), klikt u op  **Verwijder**, en klik vervolgens op **sluiten**.

![Azure Managed Cache Service NuGet-pakket verwijderen](./media/cache-migrate-to-redis/IC757666.jpg)

Verwijderen Hallo Managed Cache Service NuGet-pakket verwijdert Hallo Managed Cache Service assembly's en Hallo Managed Cache Service vermeldingen in Hallo app.config of web.config van de clienttoepassing Hallo. Omdat een aantal aangepaste instellingen kunnen niet worden verwijderd wanneer u Hallo NuGet-pakket verwijdert, open web.config of app.config en zorg ervoor dat Hallo volgende elementen zijn volledig verwijderd.

Zorg ervoor dat Hallo `dataCacheClients` vermelding is verwijderd uit Hallo `configSections` element. Verwijder Hallo gehele niet `configSections` element; alleen verwijderen Hallo `dataCacheClients` -item, indien aanwezig.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

Zorg ervoor dat Hallo `dataCacheClients` sectie is verwijderd. Hallo `dataCacheClients` sectie zijn vergelijkbaar toohello voorbeeld te volgen.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

Zodra Hallo Managed Cache Service configuratie is verwijderd, kunt u Hallo-cacheclient configureren zoals beschreven in de volgende sectie Hallo.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Een cacheclient met behulp van Hallo NuGet-pakket StackExchange.Redis configureren
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>Managed Cache Service code migreren
Hallo-API voor client hello StackExchange.Redis-cache is vergelijkbaar toohello Managed cacheservice. Deze sectie biedt een overzicht van Hallo verschillen.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>Verbinding maken met behulp van Hallo ConnectionMultiplexer klasse toohello-cache
In Managed Cache Service verbindingen toohello cache zijn verwerkt door Hallo `DataCacheFactory` en `DataCache` klassen. Deze verbindingen zijn in Azure Redis-Cache, beheerd door Hallo `ConnectionMultiplexer` klasse.

Voeg de volgende Hallo instructie toohello boven aan elk bestand van waaruit u wilt tooaccess Hallo cache gebruiken.

```c#
using StackExchange.Redis
```

Als deze naamruimte kan niet worden omgezet, moet u NuGet-pakket StackExchange.Redis Hallo hebt toegevoegd zoals beschreven in [hello cacheclients configureren](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

> [!NOTE]
> Houd er rekening mee dat Hallo client StackExchange.Redis is .NET Framework 4 of hoger vereist.
> 
> 

tooconnect tooan Azure Redis-Cache-exemplaar, aanroep Hallo statische `ConnectionMultiplexer.Connect` methode aan en geeft Hallo eindpunt en-sleutel. Een aanpak toosharing een `ConnectionMultiplexer` exemplaar in uw toepassing is toohave een statische eigenschap die een verbonden exemplaar retourneert, vergelijkbare toohello voorbeeld te volgen. Dit biedt een thread-veilige manier tooinitialize slechts één verbonden `ConnectionMultiplexer` exemplaar. In dit voorbeeld `abortConnect` is set toofalse, wat betekent dat Hallo aanroep slaagt, zelfs als er een cache van de toohello verbinding niet tot stand wordt gebracht. Een belangrijke functie van `ConnectionMultiplexer` is dat deze automatisch verbinding toohello cache herstelt, zodra het netwerkprobleem Hallo of andere oorzaken opgelost zijn.

```c#
private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
{
    return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
});

public static ConnectionMultiplexer Connection
{
    get
    {
        return lazyConnection.Value;
    }
}
```

Hallo cache-eindpunt, sleutels en poorten kunnen worden verkregen van Hallo **Redis-Cache** blade voor uw cache-exemplaar. Zie voor meer informatie [Redis-Cache-eigenschappen](cache-configure.md#properties).

Wanneer Hallo-verbinding tot stand is gebracht, het retourneren van een database met verwijzing toohello Redis-cache door de aanroepende Hallo `ConnectionMultiplexer.GetDatabase` methode. Hallo-object heeft geretourneerd van Hallo `GetDatabase` methode is een lichtgewicht Pass Through-object en hoeft niet toobe opgeslagen.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

Hallo maakt gebruik van de client StackExchange.Redis Hello `RedisKey` en `RedisValue` typen voor toegang tot en het opslaan van items in de cache Hallo. Deze typen wijzen naar de meest primitieve taaltypen, string, inclusief en vaak worden niet gebruikt rechtstreeks. Redis-tekenreeksen Hallo meest eenvoudige vorm van Redis-waarde zijn en veel soorten gegevens, waaronder geserialiseerde binaire gegevensstromen, kunnen bevatten en u mogelijk Hallo type niet rechtstreeks gebruiken, gaat u methoden die bevatten `String` in Hallo-naam. Voor de meest primitieve gegevenstypen u gegevens kunt opslaan en ophalen van items uit Hallo-cache met behulp van Hallo `StringSet` en `StringGet` methoden, tenzij u verzamelingen of andere Redis-gegevenstypen in Hallo cache opslaat. 

`StringSet`en `StringGet` zijn vergelijkbaar toohello Managed cacheservice `Put` en `Get` methoden met een grote verschil is dat de voordat u instelt en ophalen van .NET-object in de cache Hallo u het eerst serialiseren moet. 

Bij het aanroepen van `StringGet`Hallo object bestaat, wordt deze geretourneerd en als dat niet het geval is, wordt null geretourneerd. In dit geval kunt u Hallo waarde wordt opgehaald uit de gewenste gegevensbron Hallo en opslaan in cache Hallo voor later gebruik. Dit staat bekend als Hallo cache-aside '-patroon.

toospecify hello vervaldatum van een item in de cache hello, gebruik Hallo `TimeSpan` parameter van `StringSet`.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Azure Redis-Cache kunt werken met .NET-objecten, evenals de primitieve gegevenstypen, maar voordat een .NET-object kan worden opgeslagen in de cache moet worden geserialiseerd. Dit is de verantwoordelijkheid van de ontwikkelaar van de toepassing hello Hallo. Dit biedt Hallo keuze Hallo serialisatiefunctie Hallo ontwikkelaar flexibiliteit. Zie voor meer informatie en voorbeeldcode [werken met .NET-objecten in cache Hallo](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>ASP.NET-sessiestatus en tooAzure Redis-Cache van de uitvoercache migreren
Azure Redis-Cache heeft providers voor ASP.NET-sessiestatus- en pagina van de uitvoercache. toomigrate uw toepassing die gebruikmaakt van Hallo Managed Cache Service versies van deze providers, verwijdert u eerst bestaande secties uit uw web.config Hallo en configureer vervolgens hello Azure Redis-Cache-versies van Hallo providers. Zie voor instructies over het gebruik van Azure Redis-Cache ASP.NET-providers hello, [ASP.NET Session State-Provider voor Azure Redis-Cache](cache-aspnet-session-state-provider.md) en [ASP.NET-Cacheprovider voor Azure Redis-Cache](cache-aspnet-output-cache-provider.md).

## <a name="next-steps"></a>Volgende stappen
Hallo verkennen [documentatie van Azure Redis-Cache](https://azure.microsoft.com/documentation/services/cache/) voor zelfstudies, voorbeelden en video's.

